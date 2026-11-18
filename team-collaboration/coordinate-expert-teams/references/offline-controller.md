> Portable documentation export: the original offline mock scripts are not included. Test-count statements below describe the original package, not a test run of this export.

# 外部专家 CLI 控制器：离线 reference / contract tests

**这是本地协议状态机参考实现，不是已部署、已证明稳定的真实供应商集成。**
没有调用模型、读取凭据、操作远端、安装包、运行网络代理或常驻 daemon。
仅使用 Python 标准库，Linux/POSIX 本地 mock subprocess。

## 设计先于适配

真实 CLI 的协议不能由通用控制器猜测。`Adapter` 显式配置版本、result 事件名、允许的 progress 事件及独立 validator；这里仅提供 `mock-1`。
接入任何真实工具前，必须实际验证已安装版本/能力及该版本的事件、认证、订阅计费、会话语义，再实现该工具的 validator。`version` 参数目前只是测试输入，**不是自动版本探测**。

控制流程：

1. 验证版本和已知预算；unknown、NaN、Infinity、负数或不足均 fail closed。
2. 以 session ID 获取原子本地排他锁；持久化 provider/model/effort/session 身份绑定，禁止同 session 静默更换身份。
3. 写入 request intent ledger，然后启动子进程；JSONL 请求输入完成后显式关闭 stdin。
4. 并行读取 stdout/stderr；stderr 仅作诊断，不认作成功。严格识别事件，未知事件/未完整 JSONL/身份不匹配/截断均报协议错误。
5. 每个预期 turn 必须有且只有一个验证后的 result。立即原子持久化，进程不退出也不丢失已落盘结果。
6. 超时或断线，没有完整已验证结果为 `unknown`，不盲重试。相同 request ID 和输入只查询 ledger，`inflight`/`unknown` 也不重发；变更输入拒绝复用 request ID。
7. 回收 mock 子进程并释放 session 锁。最终 `exit_code` 仅提供诊断信息，不代替 result。

`success` 是**配置 adapter 的协议级成功**，不是答案正确、provider 计费停止、后端推理结束或模型完整理解输入的证明。

## Manifest 与 coverage 的边界

请求和结果都记录输入 SHA-256 / UTF-8 字节长度；结果同时记录输出 SHA-256 / 字节长度，并验证完全一致。每个 turn 的 result 均写入 ledger。

`required_coverage` 是主机期望的检查清单，mock 返回其匹配值以测试拒绝缺失/错误证据的分支；`model_says: read everything` 不被接受。**mock 的回显不构成实际 coverage 证据。** 真实适配器必须从可信主机 instrumentation 生成/核验 evidence，例如分片 manifest、每片提交 receipt、外部测试 ID/结果和引用跨度一致性；不能把 provider 或模型的自报“读全”升级为 proof。即使传输覆盖证据充分，也不能证明模型注意力或理解覆盖全部内容。

## 源实现与本发布范围

本发布仅包含设计说明，不附带 `reference.py`、`mock_cli.py` 或 `test_reference.py`，没有可运行的 `scripts/` 目录。因此不要在本包运行原版测试命令，也不能把下述历史测试数量当成本发布验证结果。

## 已知缺口 / 生产接入前门槛

- 无任何真实 provider 的能力或支持性结论；没有真实 CLI 的版本 probe、schema、resume/reconciliation API、cost meter。
- 预算是调用前已知 ceiling 的准入测试，不是运行中 token/货币硬限额；实际费用 unknown 时不可声称受控。
- bounded 小请求使用阻塞 stdin write；生产需非阻塞、有上限、纳入 deadline 的写入，以及 stdout/stderr/ledger 尺寸上限和背压。
- 本地锁不是跨机器分布式锁；崩溃遗留锁保持 fail closed，需人工/可信租约恢复。未测试断电、目录 fsync、磁盘满、持久化损坏或多机竞态。
- POSIX mock 以新进程组启动，并用 SIGTERM→SIGKILL 取消；尚未验证逃逸进程组、孙进程或 Windows Job Object。终止本地进程不等于取消远端请求。
- ledger 会保存明文输入输出，仅适合非敏感 fixture。生产需数据最小化、权限/加密、保留期和脱敏。
- `inflight` 崩溃恢复需要显式查询和人工/受控 reconciliation；没有自动重发路径，也不声称网络侧 exactly-once。
- 多轮测试为单次请求中返回多个 turn result，不代表已实现交互式 stdin 多轮协议；长期会话需要各 CLI 的具体 transport adapter。
- 版本 pin、mock 测试通过是必要设计检查，不是生产可靠性认证。


## v2：完整 Agent 任务合同与后台句柄（仍然仅离线参考）

本版本**不默认 Agent 只读**：`TaskCapabilities` 显式携带专属 task_directory、write_documents、network_search、tools、max_runtime_seconds 和 transport。测试允许 mock 在任务目录写文档，同时传递网络搜索和工具能力声明；**没有真实网络调用，也没有修改任何安全权限**。这些字段是任务合同，不是操作系统沙箱，也不会实际授予网络/凭据权限。真实运行器需要把它们映射到经过版本验证的 CLI 权限与 OS 隔离能力。

`start_background()` 立即返回 `BackgroundRun`，父线程可继续回应用户并启动其他 session 的任务：

- `poll()` 读取原子 ledger 状态，不等待结果；`wait(timeout)` 仅限本次等待，**不会因此终止 Agent**。
- `status` 表示验证后结果状态；`process_state` 和 `exit_code` 独立表示进程生命周期。结果已成功但进程仍运行是合法状态。
- stdout 事件、stderr 和退出事件按 JSONL 增量持久化；ledger 记录 supervisor `heartbeat_at`、`last_agent_event_at` 和事件数。主机 heartbeat 不是 Agent 真实进展证明。
- 没有最终文本不触发 idle kill。后台任务必须有显式有限 `max_runtime_seconds`；达到该合同 wall budget 才触发取消，不能以“无限等待”暗示无限费用授权。预算仍需已知 cost ceiling，未知预算拒绝启动。
- `cancel()` 请求取消，本地 POSIX 进程组先 SIGTERM，宽限后 SIGKILL；没有最终结果时仍是 `unknown`，不自动重发。远端工具产生的副作用不能由本地取消撤回，需供应商 reconciliation。
- `transport='one_shot'` 的输入 EOF 语义已实现；`interactive` 明确拒绝并要求专属 transport adapter，绝不假装等价。交互 session 需要逐 turn 输入、明确 turn ID、会话身份、取消和恢复协议。

### 新增验证与保留缺口

新增后台等待超时不杀任务、主线程即时返回、增量事件/心跳、目录写文档、显式取消后不重发、结果/存活状态分离、独立 session 并行、交互 transport 拒绝、wall budget 到期。新增 8 tests，加原 14 tests，共 **22 tests**。

非 daemon 的本地 Python worker 线程只是测试运行器，不是已部署持久化后台服务；父进程重启后仅有 ledger，并不自动接管活进程。活跃信号长期不变应进入 `needs_investigation`/告警流程，再按任务合同决定继续或取消；本参考尚未实现 idle 检测、外部工具活跃度校验、运行中费用计量、全局并发/资源配额、进程 PID 防复用或真正 durable supervisor。单凭持续 heartbeat 也不能无限延长 wall budget。

操作幂等性只保证本地相同 request key 不重发；Agent 内部发信、提交、支付或写远端等副作用必须另设工具权限、幂等键和审批边界。本参考从未向真实第三方请求这些动作。任何未知完成状态都先查询账本/provider，而不是换 request ID 重跑。

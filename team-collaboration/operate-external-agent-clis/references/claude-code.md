# Claude Code — verified 2026-11-13

Sources: [CLI reference](https://code.claude.com/docs/en/cli-reference), [model configuration](https://code.claude.com/docs/en/model-config), [headless](https://code.claude.com/docs/en/headless), [permissions](https://code.claude.com/docs/en/permissions), [permission modes](https://code.claude.com/docs/en/permission-modes). Reuse this baseline while applicable. Recheck only affected flags or models when a material change, observed failure or task-specific gap warrants it; do not mechanically recheck by date or on every call.

Observed version 2.1.323 supports the options below. One authorized, tool-free `sonnet`/`low` call returned the expected visible text, exit 0 and one turn, with model telemetry `claude-sonnet-5-5`. This establishes that one call only; it does not certify other models, accounts, hosts, tool use or resume. Cost telemetry is not an invoice.

## Model, effort and directory

- `--model` accepts supported aliases or full model IDs. Alias resolution can change; record the actual response model. A help listing does not prove account entitlement or current availability.
- `--effort low|medium|high|xhigh|max` is model-dependent. `CLAUDE_CODE_EFFORT_LEVEL` can override the flag; check only this relevant value, not a full environment dump. Do not invent equivalence to another provider's reasoning tokens or force `max` on unsupported models.
- Set the working directory with the shell or process `cwd`: `cd "$WORKDIR" && ...`. `--add-dir` adds filesystem scope; it does not change cwd. Do not confuse a subcommand's `--cwd` filter with a global execution-directory option.

## Minimal subscription-route call

Use only after the real call and its data destination are authorized. This Linux smoke recipe follows the observed flags; its explicit EOF is a defensive addition. Use a transport-supported deadline if `timeout` is unavailable; the 60-second limit is for this tiny smoke test, not a universal task limit. Resolve the executable and trusted directory first. Check each option in installed help.

```sh
cd "$WORKDIR" && timeout 60s "$CLAUDE_BIN" -p 'Reply exactly CLI_OK.' \
  --model sonnet --effort low --output-format json \
  --safe-mode --tools '' --strict-mcp-config \
  --permission-mode dontAsk --permission-prompts none --no-session-persistence </dev/null
```

`--safe-mode` disables customizations while retaining authentication/permission settings; managed policy remains. `--tools ''` disables built-in tools, not necessarily MCP. `--strict-mcp-config` skips MCP servers not explicitly supplied, so supply none for this test; alternatively verify an appropriate MCP disallow rule in the installed version. Verify emitted events show no tool calls. Do not change persistent configuration to obtain a clean smoke test. Omitting stdin EOF can cause a noninteractive wait. Without these controls, `-p` can load project instructions/hooks/MCP; print mode is not a read-only guarantee.

Do not use `--bare` as a generic clean subscription test: it does not read subscription OAuth and requires an API/provider authentication route. Do not switch to API billing silently when subscription invocation fails.

## Autonomous operation and YOLO

For task execution, use the full useful authorized tool set rather than the connectivity-only recipe above. See [provider execution modes](execution-modes.md), checked 2026-11-14, for auto mode and cross-provider distinctions. `--permission-mode auto` uses automatic review; it is not the same as `dontAsk` or unrestricted bypass.

- `--allowedTools` pre-approves tool usage, not an exclusive allowlist. Use `--tools` to limit the available built-in tools and verify MCP separately.
- `--permission-mode dontAsk` rejects unapproved actions rather than opening an interactive prompt; it is not YOLO.
- `--permission-prompts none` (documented from 2.1.259) fails closed for unattended approval needs; inspect `permission_denied`/`permission_denials` rather than treating an exit/result as task success.
- `--dangerously-skip-permissions` / `--permission-mode bypassPermissions` bypass Claude's internal permission prompts. Use only when the current task permits the concrete tool scope and effects, within a trusted isolated workspace when appropriate. These options do not bypass the host, MCP, SSH, OS, network or account policies, and are not a remedy for a higher-level denial. Do not set them as a global default.
- `--max-budget-usd` is estimated telemetry-based control and can overshoot; it is not a billing hard cap. Preserve current task-specific limits rather than assuming a subscription is unlimited.

## Output, progress and resumption

Use `--output-format json` for a final machine-readable result; use documented `stream-json` with required verbosity options when incremental events are needed. Validate installed help before building a parser. Save text, tool results, permission denials and terminal records separately. Do not expose raw private reasoning; show useful progress and artifacts.

Use `--resume <explicit-session-id>` for a retained session; avoid `--continue` in concurrent/shared work because it selects a recent conversation. `--no-session-persistence` intentionally removes resumption. A running print process does not automatically accept live steering; use documented input/protocol support only, and otherwise wait for the turn boundary or cancel the owned turn before resuming. Never assume writing prose to stdin mid-turn is a supported control channel.

## Live control and recovery: documented, not exercised by the smoke test

[Streaming vs single mode](https://code.claude.com/docs/en/agent-sdk/streaming-vs-single-mode), [TypeScript SDK](https://code.claude.com/docs/en/agent-sdk/typescript), and [sessions](https://code.claude.com/docs/en/agent-sdk/sessions) describe persistent streaming input and interruption. Prefer supported SDK streaming/async-iterator interfaces when already available and authorized. Hold the original stdin/control connection; a detached process with logs alone does not promise a writable steering channel. Do not edit transcript JSONL to inject control messages.

Queued messages and interrupted turns are distinct. Inspect message/interrupt receipts and negotiated capabilities; do not infer immediate interruption from an accepted message. Reinitializing a still-running supported CLI differs from starting a new process and resuming a persisted conversation. Resume restores conversation context, not a filesystem/process snapshot; an ID alone is insufficient across hosts. Preserve the same authorized work environment and verify pending permission requests after reconnecting.

Handle interrupt, process termination and remote-effect reconciliation separately. Before retrying after SSH/MCP loss, check the owned process, last terminal event and output artifacts. No advanced control, cross-host resume or cancellation behavior was validated by the tool-free connectivity call.

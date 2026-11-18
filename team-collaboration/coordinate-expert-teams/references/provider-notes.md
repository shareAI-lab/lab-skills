> Portable documentation export: the original offline mock scripts are not included. Test-count statements below describe the original package, not a test run of this export.

# Provider transport notes

Use these as design cautions drawn from research dated 2026-10-29. Recheck installed help and official version-matched sources before executing; no live provider adapter is bundled.

| Surface | Distinction to preserve |
|---|---|
| Antigravity `agy` | `stream-json` may be persistent multi-turn; validated per-turn `result` and process exit are separate. Send EOF only at intended session end, save a result immediately, then use a distinct shutdown grace. Do not import Claude's control protocol. `SUCCESS` and exit 0 can coexist with required tool soft-denials. |
| OpenCode 1.19.5 CLI | `run --format json` waits for EOF on non-TTY input. Model syntax is provider/model with a separate `--variant`; neither `step_finish` nor last text alone proves final acceptance. Pin provider identity; GitHub Copilot is not Anthropic API billing. |
| OpenCode HTTP/SSE | A dedicated authorized local server can support session/message/status reconciliation. Subscribe then dispatch, correlate IDs, and read final messages/status after a dropped stream. A 204 accepted response is not completion. Abort local HTTP is not necessarily server session abort. |
| ACP | Initialize, negotiate actual capabilities/auth, create/load exact session, send a prompt, process updates and server requests, then validate the corresponding prompt response and required tools. Keep stdin open. Permission prompts/extension requests must get a policy-valid response; never silently auto-approve. |
| Cursor CLI | Explicitly resolve the Cursor binary; do not run bare `agent`. `--print` alone is not read-only. Pick task-appropriate tools/permissions from current help; `--mode ask` is for read-only consultation, not an appropriate universal limit on authorized document-writing agents. Validate terminal result and tool evidence. |
| Grok Build CLI | Explicitly resolve Grok; its JSON format names and permission “Ask” are not Cursor's format/mode. Verify current model/effort, background, search, cancellation and resume behavior. Do not infer tool availability from another Grok product/API. |
| Claude Code | Use the companion operate-external-agent-clis reference: a 2026-11-13 tool-free call on 2.1.323 succeeded; advanced streaming/resume/tool effects remain separately unverified. Do not transplant private host/account details. |
| Codex / Gemini / Pi | This package contains no separately audited live adapter for these CLIs. Probe current commands, model/effort and protocol before use rather than guessing from brand similarity. |

## Version-pinned OpenCode steps/prefill trap

Observed with OpenCode V1 1.19.5, commit `810c0eba1a7348036f8bdf61e6632d0c36c6876c`: [`session/prompt.ts` around L1209](https://github.com/anomalyco/opencode/blob/810c0eba1a7348036f8bdf61e6632d0c36c6876c/packages/opencode/src/session/prompt.ts#L1209) appends an assistant message on the first turn when `agent.steps=1`. Claude Opus 5.5 rejected that prefill with HTTP 400. Offline replay against the prior length/aborted-write history confirmed that steps 1 changed the final role from user to assistant, while steps 2 left it user. This is version-specific evidence; the corresponding online repair is not yet verified.

Keep provider-call budget separate from agent-step semantics: do not translate “at most one response/request” into `steps=1`. For this version, use task steps at least 2 plus an independently enforced one-request provider guard, verifying that the guard actually caps calls. Recheck on version changes; do not infer that steps alone controls spending. Pass the known launcher, pinned version, and this trap to every executor at handoff rather than rebuilding configuration per task and repeating an already diagnosed failure.

## Sources for revalidation

- Antigravity: [Headless](https://antigravity.google/docs/cli/headless/), [CLI reference](https://antigravity.google/docs/cli/reference/), [Permissions](https://antigravity.google/docs/permissions/), [Official changelog](https://github.com/google-antigravity/antigravity-cli/blob/main/CHANGELOG.md).
- OpenCode: [CLI](https://opencode.ai/docs/cli/), [Server](https://opencode.ai/docs/server/), [SDK](https://opencode.ai/docs/sdk/), [ACP](https://opencode.ai/docs/acp/), [Permissions](https://opencode.ai/docs/permissions/), [v1.19.5 source](https://github.com/anomalyco/opencode/tree/v1.19.5).
- Cursor: [Parameters](https://cursor.com/docs/cli/reference/parameters), [Output format](https://cursor.com/docs/cli/reference/output-format), [ACP](https://prod.cursor.com/docs/cli/acp), [Permissions](https://prod.cursor.com/docs/cli/reference/permissions), [Changelog](https://cursor.com/docs/cli/changelog).
- Grok Build: [Headless](https://docs.x.ai/build/cli/headless-scripting), [CLI reference](https://docs.x.ai/build/cli/reference), [Permissions](https://docs.x.ai/build/features/permissions), [Sandbox](https://docs.x.ai/build/features/sandbox), [Changelog](https://x.ai/changelog/build), [Official public source](https://github.com/xai-org/grok-build).

Do not treat a forum report or older source revision as proof of a current installed bug. Separate native web search, fetch, X search, and research workflow support, and verify real tool events/sources for each needed capability. API capability does not imply subscription coverage or availability in a different harness.

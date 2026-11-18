# Headless execution modes — checked 2026-11-14

Use only the applicable section. These are capability references, not grants of access. Reuse verified target-machine adapters; check installed help when its version or wrapper identity differs. Official documentation verification is not a live model/tool test.

## Claude Code

Sources: [CLI reference](https://code.claude.com/docs/en/cli-reference), [permissions](https://code.claude.com/docs/en/permissions).

`-p` is headless execution. `--permission-mode auto` uses automatic classification/review; it is not unrestricted bypass. `--dangerously-skip-permissions` / `--permission-mode bypassPermissions` skips ordinary CLI permission prompts, subject to documented exceptions and managed/environment policy. Use only for the authorized scope, with appropriate external isolation. `--permission-mode dontAsk` denies unapproved calls, not full autonomy. Plan mode is not an execution substitute.

`--tools default` enables the default built-in set; `--tools Read` restricts availability. `--allowedTools` pre-approves matching uses, rather than defining the entire registry. MCP availability/permissions are separate. `--permission-prompts none` (documented since 2.1.259) denies remaining approval needs instead of hanging. Record those denials. Set cwd in the process/shell; `--add-dir` extends access, not cwd. See [Claude detail](claude-code.md) for models, output and resumption. Do not copy the tool-free smoke recipe into real delegated work.

## Codex

Sources: [non-interactive mode](https://learn.chatgpt.com/docs/non-interactive-mode), target-installed `codex exec --help`. Locally inspected CLI: `0.167.0-alpha.4`; only version/help were run, no inference.

Use `codex exec`, `-C DIR` for working root, `-m MODEL`, `--json` for events and `-o FILE` for final text where installed help supports them. Current docs no longer support `--full-auto`; do not perpetuate that stale recipe. `--sandbox workspace-write` supplies bounded writes; `--approve-for-me` routes requests through automatic review with workspace-write, not blanket permission. Check network and approvals separately for the target configuration. `--add-dir` adds writable roots, not read-isolation.

`--dangerously-bypass-approvals-and-sandbox` removes both controls and is explicitly intended for externally sandboxed environments. Do not use it merely to defeat a managed denial or assume a task folder provides that external sandbox. Resume an explicit retained session, not `--last` in a multiworker environment. Do not read protected session storage to recover it.

## Gemini CLI

Source: [configuration reference](https://geminicli.com/docs/reference/configuration/).

Use `-p` for headless work. `--approval-mode=yolo` auto-approves tools; `auto_edit` covers edits, not all tools; `plan` is read-only. Do not combine `--yolo` and `--approval-mode`. `-m` chooses model; `--include-directories` adds workspace scope. Docs describe YOLO sandbox behavior, but verify the actual installed platform/backend before claiming isolation. No general `--effort` flag was established from the inspected official reference: resolve wrappers or other binaries before borrowing that option. Model and CLI branding alone do not establish executable identity or supported flags.

## OpenCode

Sources: [CLI](https://opencode.ai/docs/cli/), [permissions](https://opencode.ai/docs/permissions/).

Current official V2 documentation uses a `permissions` list with `action`, `resource`, `effect`; V1's `permission` map and `bash`/`task` naming are not interchangeable with V2 `shell`/`subagent`. Last matching rule wins; unmatched requests ask. Match the installed version before constructing task-scoped allow rules for unattended work. Do not transplant a legacy environment/config snippet without verification.

`run` is headless. V2 documents a shared per-user background server owning sessions, configuration, permissions and tool execution, with `--standalone` for a private server. Consider that server boundary, inherited settings and distinct sessions when assessing independence; cwd alone is insufficient. Avoid starting or changing persistent shared services just for a consultation. A private server does not by itself create OS filesystem isolation.

## Other CLIs and wrappers

For Cursor, Grok Build, Pi and other names, resolve the exact executable/vendor/version and its relevant official help before prescribing flags. Do not infer YOLO, model names, effort, search or session APIs from another CLI. Mark unknown cells explicitly. Add a compact verified adapter only when real task demand justifies it; preserve budget, account and data-sharing boundaries.

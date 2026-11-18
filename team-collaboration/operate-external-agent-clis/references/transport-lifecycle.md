# Transport and lifecycle

## Shell transport is not an agent protocol

MCP/remote/SSH usually supplies command execution; the installed CLI remains the provider client. Discover the actual shell, OS user, container, filesystem roots and transport timeout. Do not assume a shell on device A shares files, environment, credential stores or session IDs with device B.

Use argument arrays with `shell=false` when the transport supports them. Otherwise pass a carefully quoted fixed launcher and provide the prompt through stdin or a task-local input file, not shell interpolation. Avoid secrets in argv, logs, shell history or exported context. Transfer only authorized source material; verify file length/hash and readback where completeness matters.

For one-shot input, finish and close stdin. For persistent JSONL/ACP, follow that protocol's session lifecycle instead; premature EOF can terminate useful work. Drain stdout and stderr, save complete terminal records and preserve partial evidence without calling it complete. Parse the installed version's output, not another provider's event names.

## Task record

Keep these fields local to the job, excluding credentials:

```
request_id / attempt_id / owner
transport / device identity / OS user / container
binary / version / model requested and observed / effort requested and observed
workspace / allowed writes / tools / approved external effects
source ranges and gaps / prompt artifact
start / deadline or stopping condition / budget boundary
process handle / session ID / last real event
terminal event / exit / answer / artifact / acceptance / delivery
```

A CLI may emit a session ID even when session persistence is disabled. Resume only an explicitly identified retained session. Avoid bare “continue latest” when more than one worker shares the same account/directory.

## Background work and retries

Use an already-authorized supervisor or the transport's supported background facility. Keep a durable job handle and artifacts on the execution device. Shell survival after SSH disconnect does not prove model progress or provider cancellation. Do not add a competing scheduler, daemon or startup service.

After timeout/disconnect, classify outcome as unknown until checked. Recover existing output/status before resubmission; do not spend another model call just to inspect a file. Record how to cancel the exact owned job and whether provider-side effects remain unknown.

## Other providers

Reuse a verified adapter when it covers this task. Inspect the relevant `--help`, model listing or official documentation only for a new CLI or a material task-relevant gap. Codex, Gemini, OpenCode, Pi, Cursor, Grok and Antigravity have distinct CLI syntax and lifecycle semantics. Resolve the full binary path where generic names such as `agent` collide. Model family diversity is not guaranteed by using different CLI brands. Keep subscription and API routing explicit; do not translate an “agent steps” setting into a provider-call spending cap.

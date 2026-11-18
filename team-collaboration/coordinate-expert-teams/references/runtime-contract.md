> Portable documentation export: the original offline mock scripts are not included. Test-count statements below describe the original package, not a test run of this export.

# Runtime contract

## Preflight gate

Record the exact executable path and version, model/effort support, adapter version, protocol, OS, existing identity label, auth-route type (never token), relevant effective-config hashes, workspace, tools/network scope, context manifest, and resource/budget ceilings.

Probe using current help, documented status/model-list capabilities, and official version-matched documentation. A listed model does not prove the account can invoke it. Do not use a real model prompt as a supposedly free health check. If subscription inclusion, additional credits, or identity is unresolved and material to the user's limit, stop dispatch and surface the missing approval/evidence.

Do not import “highest effort” strings from one CLI into another. Do not silently fallback providers, models, accounts, subscription routes, or paid APIs. Account identity is not reliably inferred from a separate CLI's login.

## Reasoning and visible-output budget

Inspect how the installed adapter maps the chosen effort to reasoning tokens, total output, visible-text allowance, provider caps, and per-turn limits. Use help/config/schema/read-only evidence first; a new model experiment requires the current task's authorization and budget. Do not assume different names or numeric limits are equivalent across providers.

Reserve a viable path to a concise visible answer or verifiable tool artifact. If a turn ends with `length` or a full reasoning budget and empty text, mark the visible answer as missing, not accepted advice; check whether a required tool artifact exists and whether it is complete. Inspect existing tool outputs separately: a file may exist despite empty final prose, and prose may claim a file that was never written. Check contents, version and scientific/task correctness independently. Record unknown budget mapping rather than claiming it is controlled.

Prefer high-effort quality where justified, not `max` as a ritual. Do not blindly repeat the same expensive request, raise limits, silently lower an explicitly requested effort, or switch billing/model routes. Diagnose the mapping and propose or make only already-authorized bounded adjustments. Client token/cost estimates are telemetry, not billing receipts.

## Context readback and staged delivery — recommended practice

A bounded recovery worked in one observed Claude Opus 5.5 case: keeping XHigh and the 48K limit, one same-session request for direct visible text (at most 900 Chinese characters), without a huge write or full-context resend, returned 769 characters covering five candidates. **Case evidence, not a general guarantee:** the draft still contained a scientific error, so delivery success is not research correctness. A failed large-output run does not establish that its effort setting is permanently unusable; retain specified effort unless a change is authorized.

- Before major synthesis, request a concise context-coverage readback of the original requirements, source ranges actually available, constraints, and ambiguities. Check it against the source manifest and user messages, not merely the agent's assertion of full coverage. Self-reported truncation or a requirement misreading blocks content acceptance even when the transport reports `SUCCESS`.
- Stage a substantial deliverable: first obtain a visible roughly one-page core proposal, then deepen each alternative in bounded sections. Save and inspect each artifact as it arrives. Avoid making one enormous tool write the only delivery path, and do not spend another full request solely to confirm whether a prior write succeeded; inspect the existing artifact and tool result first.
- Numeric output allowances and high effort do not guarantee visible content. A `max_tokens` terminal plus an aborted write may leave no deliverable. Reasoning/non-reasoning token counters are telemetry, not proof that prose or complete tool arguments were delivered. If raw arguments were not retained, do not claim to have observed truncated JSON or reconstruct its contents. Exit codes and success labels likewise do not replace tool-result and content checks.
- Keep original received drafts/artifacts separate from the lead's review and corrected synthesis, within authorized retention limits. Mark partial, thinking-only, timed-out, or unverified outputs accurately; preserve useful evidence without promoting an unfinished recovery attempt to a proven workflow.

## Lifecycle

Track separately:

| Dimension | Evidence required |
|---|---|
| Submitted | Durable intent plus transport-specific send/acknowledgment |
| Turn terminal | Validated provider event/response for the correct session and turn |
| Required tools settled | Real tool results; soft-deny/failure still blocks required work |
| Visible deliverable | Nonempty answer or verified tool-produced artifact, not reasoning-only usage |
| Answer accepted | Content/scientific/task-specific validation of the actual output |
| User-accessible delivery | Correct current version at the verified authorized entry; upload alone is insufficient |
| Context coverage | Host manifests, source ranges, receipts and selected source checks |
| Process cleanup | Owned process/session status and no outstanding required handles |
| Billing/cancellation | Provider/account evidence where available; otherwise unknown |

Suggested state names are `preflight`, `ready`, `dispatched`, `streaming`, `reconciling`, then `completed`, `partial`, `blocked`, `failed`, `cancelled`, `timed_out`, or `unknown`. Keep process state independent; a persistent transport need not exit per turn.

Use argument arrays with `shell=false`, not shell interpolation of prompts. Bound stdin writes, each frame, total stdout/stderr, disk/log volume, and wall time. Drain stdout and stderr concurrently. Decode streamed UTF-8 incrementally and reject malformed/oversized frames according to the versioned adapter. Preserve diagnostics without interpreting arbitrary stderr text as a model result.

For one-shot transports that read stdin, finish the input and explicitly close it. For persistent JSONL/ACP, preserve stdin until its documented session end; do not reuse one-shot EOF behavior blindly. Parse incrementally and atomically save validated results before waiting for shutdown. Unknown requests must be handled explicitly under the negotiated protocol, not ignored until they hang.

## Background execution

Use the authorized scheduler/supervisor, not a blocking SSH connection as task lifetime. Persist a handle with owner, job ID, exact process/session ID, workspace, ledger path, start/deadline, last agent event, heartbeat, and terminal evidence. A successful detached shell probe proves shell survival only, not model progress, remote cancellation, or completed deliverables.

A caller's `wait(timeout)` bounds that wait, not the worker's lifetime. Return to useful lead work between checks. A wall deadline must not be extended indefinitely by heartbeats. Distinguish CPU/process liveness, genuine tool/agent activity, and final result. Investigate missing progress; do not kill merely because no prose tokens appeared.

Reserve and release resources through the existing unique scheduler. Respect its current concurrency, CPU, RAM, disk, network, quota, and owner rules; do not invent limits or run a parallel scheduler. If those rules are unavailable, ask or inspect the authoritative configuration before resource-intensive dispatch.

## Recovery and cleanup

- Serialize a session; pin provider/model/effort/identity and reject accidental changes.
- Use local request IDs to avoid local resend, but do not claim vendor-side exactly-once billing.
- Retry automatically only when the task contract permits it and evidence establishes no prior submission, or a provider explicitly documents a safe retry condition.
- After submission with no reliable terminal, mark `unknown`, query the same session/ledger/provider state, and reconcile existing effects before a new attempt.
- Keep a valid answer even when process cleanup fails; label both facts. Do not repeat a paid request just to get a cleaner exit.
- Cancel through the transport when verified; then terminate only the owned process group/container if necessary. Never global-`pkill agent` or kill a shared provider leader.
- Verify remaining processes and reconcile external tools. Local cancellation cannot undo messages, payments, remote writes, or a request still running on a provider.
- Preserve minimal useful failure evidence and clean temporary sensitive data according to the task's retention policy.

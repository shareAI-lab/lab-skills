---
name: coordinate-expert-teams
description: Coordinate external CLI agents and native subagents as an evidence-backed expert team for high-value research, design, writing, complex decisions, or repeatedly stalled work. Use proactively when independent proposals and cross-critique can materially improve quality, or when the user asks for multiple models, 外部小弟, 专家团队, 独立提案, or 交叉批评. Probe current capabilities and authorization, delegate bounded tool-capable tasks, and integrate verified results without treating this skill as new spending or data-sharing permission.
---

# Coordinate Expert Teams

Follow the current user's communication preferences. Retain exact provider/model identities in technical records.

## Establish scope before dispatch

- Treat this as a reusable working method, not a production-certified provider integration or a grant of permissions.
- Use a small team only when the expected quality gain justifies its latency, exposure, and authorized cost. Do not fan out trivial work merely to use available models.
- Define the decision, audience, deliverable, acceptance tests, source material, permitted external destinations, budget, deadline, and stopping condition. Preserve the user's language and requested destination.
- Distinguish planning from execution using the latest task-specific authorization. If the user retains a selection gate, wait for that selection; if they explicitly delegate selection and execution after review, carry out the authorized reviewed work. Never impose an obsolete selection gate or infer new authority from this skill.
- Never infer authorization for new API billing, credits, subscriptions, account switching, OAuth, provider data sharing, remote deployment, or expanded tool permissions from skill installation. Apply the current task's instructions and permission boundaries to every agent.
- Read [references/environment.md](references/environment.md) when recording the recipient's authorized machines/CLIs; no private machine inventory is bundled.

## Preserve breadth before concise delivery

- **Short delivery must not mean narrow understanding.** Revisit original messages paragraph by paragraph and across turns; preserve conditions, comparisons, evolving scope, implicit assumptions and inspiration branches. Separate user intent from interpretation. Give experts direct authorized access to continuous source messages and verbatim decisive passages, including relevant earlier context; summaries are navigation, not substitutes. Record access/range gaps and test readback against the sources: transferred ZIPs, hashes and “read all” claims do not prove understanding.
- Do not turn open questions into the lead's preferred product identity, familiar architecture, A/B choice, or narrow engineering checklist. Keep proposed framing separate from the neutral source brief; do not reward experts for confirming it. Existing mechanisms can have substantial combination and engineering value; novelty of terminology is not the acceptance test.
- Repeated correction triggers a source-level omission/drift audit, not another paraphrase. On rejection, reopen the affected work and rebuild from original sources without inheriting old rankings; do not keep asking the user to select rejected options. Retain deferred inspiration as exploration, not automatic tasks, and preserve earlier proposals and the reasons for changing them.

## Preserve the meaning between the keywords

Read relationships, examples, contrasts, counterfactuals, repeated dissatisfaction and changes across messages, not just explicit nouns. Keep direct requests, supported implicit possibilities and your own new hypotheses distinct. For an important inferred possibility, retain the source and why it may matter; uncertainty is a reason to test or label it, not silently discard it or present it as the user's commitment. Treat voice-recognition ambiguities as unresolved where they would change the design.

Pursue substantial user and engineering value with natural, elegant mechanisms. Neither a novel label nor complexity proves innovation; neither familiarity nor lack of consensus disproves it. Preserve bold alternatives that survive scrutiny. When a premise fails, seek a stronger construction serving the original ambition rather than automatically settling for the safest average.

## Select the team deliberately

1. Appoint the parent as accountable lead: own task decomposition, permissions, evidence, integration, user communication, and completion.
2. For hard research/design/writing, choose the number of genuinely distinct experts or lenses that the task warrants; there is no default mandatory team size. Prefer distinct underlying model families when available; two harnesses calling the same model are not independent models.
3. Give the strongest suitable, authorized model the hardest planning/synthesis work. Prefer its highest **actually supported** reasoning/effort level only with a workable reasoning/output budget for that CLI, model, transport, and account. Probe rather than guessing `max`, `xhigh`, or cross-vendor equivalents; `max` is not proof of the best answer. Preserve enough budget for a visible result, inspect the actual mapping, and do not silently change a specifically requested effort. Do not upgrade a subscription or spend extra credits to meet this preference.
4. Give a fast executor a narrow, explicit contract after a design exists. Do not substitute a fast model's unreviewed judgment for unresolved architecture or research decisions.
5. Keep provider, exact binary path/version, actual model, effort, identity label, and session explicit. Record unknown identity or silent model fallback as a gap, not as successful diversity.
6. If external execution is blocked, continue authorized local planning, use available native subagents where appropriate, and report exactly what remains unverified. Do not pretend a mock test is an external expert opinion.

## Close the loop without making the user manage the team

1. **Anchor the work:** retain the original goal/acceptance and latest valid constraints. Classify each new message as a supplement, replacement, new parallel task, or exploration. A new topic does not cancel old work; an exploratory idea is not automatically a commission. Do not let an older broad instruction override a newer specific pause or selection gate.
2. **Check, then synchronize:** inspect the existing native task/session before dispatching. Keep one accountable owner and canonical task entry; send relevant goal/constraint/version changes to affected executors, and verify they are working against that version. Do not launch a duplicate to compensate for missing progress or an undelivered result. For native subagents, `send_message` delivers context but does not start an idle/interrupted turn: use `followup_task` on the same agent when authorized work must resume, then verify running state and actual acknowledgement/result; do not equate delivery with execution. For other task tools, inspect their documented resume semantics instead of transplanting this API.
3. **Keep distinct evidence:** record execution state, actual artifact/visible output, content acceptance, and user-accessible delivery separately. A completed task badge, a generated file, an upload receipt, and satisfaction of the original goal are not interchangeable. Verify the final version and entry point; propagate corrections to the existing deliverable/index rather than leaving the user at an obsolete copy.
4. **Use one progress view:** use native task/session/artifact records as truth and derive one human-readable progress view from them. Do not maintain competing hand-updated Todo systems. Keep original goal, owner/entry, latest constraint, evidence, next step, and waiting condition linked; report only substantiated progress and useful result links, not internal coordination/storage mechanisms or paths.
5. **Own the open ends:** continue authorized independent work while blocked. Keep important pending choices and delivered-but-easily-missed results visible at natural intervals with the original entry and a concise recommendation/trade-off. No-change polling is not a new update. Silence is neither approval nor cancellation; do not resume gated work or turn every exploration into a reminder.

## Keep the lead responsive and the delivery short

- Stay available across workstreams. Deliver useful findings and artifacts in batches rather than waiting for every branch to finish; do not claim work continues in the background without a real active task/handle.
- Research deeply but deliver briefly: default to **1–2 pages, at most 3 unless explicitly requested otherwise**. Keep Markdown as the working source; do not default to PDF/Word. This compresses delivery, not the depth of research or evidence collection. Retain the decision, reasons, strongest counterexample, uncertainty, and next step; keep detailed evidence available without burying the answer.
- For hard concepts, proactively delegate a bounded parallel visual explanation using **`explain-with-images`** when available: a lively generated illustration, comic, or cutaway rather than decorative cards. Use precise SVG/code-native figures where exact relationships require them. Verify the actual image and labels; deliver the substantive answer without waiting for the artwork. Follow the current generation/permission boundary, not a new paid API route.

## Choose collaboration shape for the task

Own the choice of whether to use a team, communication topology, goals, rounds, CLI/model mix, call counts, prompts and perspectives within the current authorization. Do not make the user manage this machinery. Reconsider the shape when evidence or task needs change, rather than completing rounds for their own sake.

This is a toolbox, not a fixed sequence. Match roles, topology, order and depth to the goal: direct execution for simple work, independent exploration for open product questions, or derivation/test/review loops for scientific uncertainty. Source fidelity, evidence, authorization and delivery acceptance remain invariant. Use the rounds below only when useful; proposal counts and review rounds belong to the current task contract, never a universal ritual.

## Independent proposals and cross-critique when useful

### Round A — independent proposals

Give each expert the same neutral task brief and necessary source bundle, its distinct lens, and the task-local contract in [references/task-contract.md](references/task-contract.md). For parallel product, engineering or model architecture design, each expert should independently construct an end-to-end proposal from equivalent authorized original context; a distinct lens is not a fragment-only assignment. Do not show another expert's answer, the preferred conclusion, or a hidden expected result before first drafts. Freeze those drafts before review, record context gaps, and distinguish retained-context experts from fresh-session blind reviewers.

Honor the latest explicit proposal count for the current task; never carry an earlier five-per-expert requirement forward as a permanent rule. Observe substantive information gain and quality rather than equating proposal count with quality. Where the user permits adaptive counts and extra proposals are redundant or weak, ask each expert for one strongest construction plus its strongest counterexample instead. Apply this equally to model experiments and network design, retaining independent first drafts and sufficient authorized original context. Do not retroactively discard accepted candidates or alter existing readiness, resource-review, budget or execution gates. Ground model designs in concrete state/tensor shapes, network connectivity, forward computation, loss and backward gradient paths, assumptions, and worked derivations/counterexamples. Distinguish claimed capabilities from computed or tested evidence.

Request a concise artifact containing:
- recommendation and alternatives;
- key assumptions, uncertainty, and missing inputs;
- source-backed findings with locators/URLs and retrieval dates where relevant;
- concrete plan, failure modes, and acceptance checks;
- changes made, produced file paths/hashes, and unresolved blockers.

Ask for useful rationale, not private chain-of-thought. Permit tools, network research, local code, and document creation **when the task contract and existing environment authorization allow them**; do not reduce every expert to read-only chat. Assign a dedicated workspace and named write paths. Leave credentials, unrelated user data, shared configuration, and remote side effects outside that contract unless explicitly authorized.

### Round B — cross-critique

After independent proposals are saved, give each reviewer the full candidate set for the decision and its relevant evidence. When ranking, anonymize authors and vary candidate order where practical; retain criterion-level evidence, uncertainty, ties and disagreements rather than treating model identity or average rank as validation. Ask each reviewer to identify the strongest alternative, specific factual/logic/test defects, consequences, and a falsifiable correction. Seek the strongest repair that preserves the original goal, with calculations/tests where applicable; distinguish repairable defects, unresolved hypotheses and unacceptable constraints. If no repair is known, retain the defect and a discriminating test instead of inventing a fix or silently shrinking the goal. Preserve real disagreements and ambition; do not average proposals or let accumulated risk lists flatten them into a timid compromise. Review may conclude that an original should remain unchanged. Do not ask for performative consensus or an unbounded debate.

If one material uncertainty remains, assign a focused source check, experiment, or adjudication task within the same budget. Stop when acceptance criteria are met, the decision is stable, or a required input/authorization blocks progress. Explain the unresolved decision instead of manufacturing unanimity.

### Round C — lead integration

- Verify decisive claims against original sources, tests, or artifacts; distinguish observation, inference, proposal, and unknown.
- Resolve by evidence and suitability, not majority vote or model prestige. Verify citations actually support the claim and the claimed artifact exists. Treat a synthesis or revision as a new candidate, not an automatic winner: compare it with the frozen originals under the same acceptance criteria and make gained and lost capabilities explicit. Check this convention on subsequent authorized work using verified fixes, regressions and goal retention; do not claim benefit merely because the workflow was followed.
- Preserve original, revised, failed and abandoned designs with sources, variants and reasons; a new recommendation must not erase the old one. Preserve valuable dissent, limits, trade-offs, and the decision rationale in the final synthesis.
- Before delivery, map every original question/relationship to the actual answer, added capability or engineering value, and supporting computation/test; flag omissions rather than substituting file existence for acceptance. Validate each executor's artifact and permissions compliance before merging or delivering. Never treat “done” in natural language as proof of a write, test, search, publication, or payment.
- Deliver the result and material caveats, not raw transcripts or secrets. Use the relevant writing/document/site skill for the requested final artifact.

## Operate external agents reliably

Read [references/runtime-contract.md](references/runtime-contract.md) before a real CLI dispatch and [references/provider-notes.md](references/provider-notes.md) for the selected transport. They describe a contract, not a ready-made production adapter. For cross-device shell/MCP/SSH operation, unfamiliar CLI discovery, live steering and evidence-driven adapter maintenance, use the companion **operate-external-agent-clis** skill when available. Keep device inventories and account-specific receipts in private task records, not in either portable skill.

- Perform read-only preflight: resolve the exact executable, version/help, supported model/effort, transport, existing auth route, permitted tools, effective configuration, subscription/budget boundary, and installed adapter evidence. Never copy tokens to probes, bundles, logs, or this skill.
- Use the CLI as a tool-capable Agent where supported, with sustained interaction within each phase. Start a fresh session for a genuinely new independent proposal phase to avoid inherited rankings; retain its sources and link prior artifacts separately. Segment output, not input evidence. Enforce one in-flight turn per explicit session. Pin the identity and input manifest. Do not use ambiguous “latest session” or bare `agent`; Cursor and Grok may collide.
- Write a dispatch ledger before sending. Keep request/attempt/session/turn IDs, context hashes and acknowledged ranges, result path, runtime limits, status, and provenance. Minimize stored input/output and apply the user's retention/privacy constraints.
- For authorized long work, return a background handle promptly while the lead remains available. Use the existing single scheduler where one exists; do not create a competing daemon or scheduler.
- Separate turn completion, process liveness, required-tool success, input coverage, visible text/tool-produced artifact, answer quality, and accessible delivery. Save valid results as they arrive; a model can spend its entire output budget on reasoning and return no answer, or write a report whose science is still wrong. Inspect both visible output and actual tool artifacts independently; do not wait for process exit to preserve them.
- Derive task-level stopping conditions, wall/output/resource protections and spending boundaries from the latest authorization and actual platform limits. Do not invent a universal turn/CU ceiling or preserve a superseded fixed ceiling when the user requests no arbitrary cap; provide an auditable plan and observable stop conditions instead, without authorizing new paid capacity. A short polling/wait timeout does not cancel the task. Silence during reasoning is not failure; heartbeats are not proof of progress. Investigate stalled signals and respect the actual task deadline.
- On unknown outcome after dispatch, inspect the existing ledger/session/provider state before any retry. Never change request ID merely to repeat an uncertain paid or side-effecting action.
- Cancel only owned processes/sessions, reconcile remote effects, and verify cleanup. Local process termination does not prove server-side cancellation or zero cost.
- Do not broaden permissions, install a new plugin, switch billing routes, or disable safeguards to make a hanging CLI work.

## Keep research history meaningful

- Separate operational run/check records from substantive research versions. Commit only a meaningful increment: new evidence (including informative negative results), a repair, an argued decision, a justified research direction, or valuable new/changed material. Dense meaningful commits are welcome; unchanged polling, timestamps, heartbeat logs, and repeated status summaries are not research progress.
- Inspect the actual diff before committing. Explain **why**, what changed and its incremental value, source references or provenance (including indirect citations where relevant), validation, and remaining limits in a proportionate commit message. Preserve the decision rationale and supporting evidence, not private chain-of-thought; verbosity cannot substitute for meaningful change.
- If repetitive no-value commits appear, trace their producing threads, scheduled jobs, or templates and correct the authorized source of recurrence rather than only cleaning symptoms. Keep required operational logs in their appropriate records, not as automatic repository commits.
- Preserve original evidence, valuable failed experiments, and informative negative findings. Any history cleanup must be authorized, recoverable, and respectful of shared history: retain a recovery reference and inspect dependencies before rewriting; do not silently force-push or erase provenance. This guidance does not itself authorize altering a project or its automation.

## State evidence honestly and keep it portable

Read [references/evidence-and-loading.md](references/evidence-and-loading.md) before claiming reliability or reuse across sessions. Maintain separate evidence for documentation, version probes, offline fixtures, real prompts, tool/artifact use, resume/cancel, detached survival, and workload acceptance. “Installed skill,” “CLI runs,” “handshake passes,” and “production-ready workflow” are different claims.

The original coordination package describes offline mock-only contract tests. Those scripts are not included in this documentation export. See [references/offline-controller.md](references/offline-controller.md) for the reference design and its limits; do not treat it as a production provider launcher.

For a child task, pass this skill's resolved path/package and the task contract explicitly if the child does not already have skill discovery. For an external harness, use its currently documented loading mechanism or include a minimal relevant instruction excerpt in the authorized task payload. Personal-skill installation alone does not configure external CLIs. Do not deploy files to remote harnesses or modify global instructions without task-specific authorization.

## Improve through observable work

When feedback repeats, trace the failure from original request through source selection, dispatch, execution, synthesis and delivery. Fix the responsible step; remove or revise conflicting and obsolete guidance rather than endlessly adding rules. Inspect existing authorized recurring checks before changing them and avoid duplicate schedules. Verify the saved change and separately test its effect on a real next deliverable: did it preserve explicit and implicit intent, choose proportionate collaboration, ground the decisive claims, and finish the authorized outcome? A saved preference or passing formatting test is not proof of behavioral improvement. Keep the user's update short and specific.

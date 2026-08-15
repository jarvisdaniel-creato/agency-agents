# Workflow Example: NDIS Behaviour Support Package

> A seven-agent clinical documentation pipeline for Australian NDIS positive behaviour support: gather → assess → plan → comply → measure → review → correspond, with fail-closed evidence handling at every step.

## When to Use This

Use this workflow when a behaviour support practitioner needs a defensible document package for a participant — a functional behaviour assessment, an interim or comprehensive behaviour support plan, and the compliance and correspondence work that surrounds them — built from the participant's actual records rather than from template boilerplate.

The workflow assumes a registered behaviour support practitioner is in the loop. Every agent drafts, structures, checks or analyses; the practitioner assesses, decides and signs. Nothing in this pipeline replaces clinical judgement, state/territory authorisation processes, or NDIS Commission lodgement.

## Agents Used

| Agent | Role in the pipeline |
|-------|----------------------|
| NDIS Case Evidence Orchestrator | Sweeps the record system and document store, reconciles sources, produces the evidence ledger everything else cites |
| NDIS Functional Behaviour Assessor | Turns the ledger into an FBA: hypothesis statements with provenance and confidence |
| NDIS Behaviour Support Plan Author | Turns the FBA into an interim or comprehensive plan with function-matched strategies |
| NDIS Restrictive Practices Officer | Classifies practices found anywhere in the work, tracks authorisation/reporting state, feeds the plan's RP sections |
| NDIS Behaviour Data Analyst | Designs the plan's ongoing measurement, then analyses the data at review time |
| NDIS Behaviour Support Reviewer | Audits the drafts before sign-off; runs the plan-effectiveness review months later |
| NDIS Practice Documents Generalist | Progress reports, monitoring letters, prescriber correspondence around the package |

## The Pipeline

```text
1. Orchestrator   → evidence ledger + coverage statement + conflict list
2. Assessor       → hypothesis statements + evidence gaps   (reads: ledger)
3. Author         → draft interim or comprehensive plan     (reads: FBA handover)
   ├─ RP Officer  → classification + compliance state for every practice
   └─ Analyst     → measurement plan + recording forms for the plan's goals
4. Orchestrator   → corroboration pass over the draft's claims index
5. Reviewer       → severity-graded findings report          (reads: draft + corroboration)
6. Practitioner   → resolves findings, decides, signs, lodges
7. Analyst        → phase-change analysis at review date
8. Reviewer       → plan review: goal scores + recommendation
9. Generalist     → progress report / monitoring letters as the cycle demands
```

**Session protocol — the first turn of any job that names a participant is
the bind-and-confirm card**: participant details, the record-system contact
link, and the client-folder directory, confirmed by the practitioner before
any substantive work by any agent. No urgency waives it; a session whose
first substantive turn is anything else has already gone wrong.

Order matters in three places: the Orchestrator always runs first (no agent drafts from an unswept record); the Reviewer sees drafts *before* the practitioner signs (so the audit happens when it is cheap); and the Analyst appears twice (designing measurement at planning time, analysing it at review time).

## Handover Artifacts

Each arrow in the pipeline is a named artifact, so agents consume each other's output instead of re-deriving it:

| Artifact | Producer → Consumer | Must contain |
|----------|--------------------|--------------|
| Evidence ledger | Orchestrator → all | Per fact: value, source(s), dates, conflict/flag status; coverage statement; searched-absence trails |
| FBA handover | Assessor → Author | Hypothesis statements (with confidence + supporting/contrary evidence), operational definitions, skill assets, unresolved questions |
| Practice register rows | RP Officer → Author, Reviewer | Per practice: category, authorisation state, plan inclusion, reporting state, fade step, next due date |
| Measurement plan | Analyst → Author, team | Per behaviour and goal: measure, form, recorder, QA check distinguishing "no incidents" from "no recording" |
| Authoring log | Author → Reviewer, practitioner | Per section: what it is based on, what was flagged, what the practitioner must verify |
| Claims index | Each drafting agent → Orchestrator | Every claim in the draft mapped to its individual evidence item (per claim, never per group) |
| Corroboration results | Orchestrator → Reviewer | Join check (claim → existing ledger entry), block-citation flags, semantic spot-checks of high-stakes claims |
| Run record | Every handover → next agent, practitioner | One line per step completed: actor (script / agent / human, named), one-line result. Appended at each hop, never rewritten |

Every handover carries the run record — a compact statement of what has been
done and by what kind of actor, so verification can distinguish a mechanical
result from a model's judgement at a glance:

```text
RUN RECORD — P-114, comprehensive BSP
1. census + manifest   script  dd_census.py        12 objects, 41 files, 2 UNREADABLE
2. read + ledger       agent   orchestrator        ledger v1 — 214 facts, 3 conflicts
3. hypotheses          agent   assessor            2 courses proposed, 1 gap open
4. draft + claims idx  agent   author              61 claims indexed
5. claims join         script  dd_corroborate.py   exit 0 — 9 queued for spot-check
6. spot-check          agent   orchestrator        9/9 verified against source
7. render              script  renderer            NOT YET RUN
Awaiting human: course confirmation, RP determination, sign-off
```

Steps done by scripts cite the script and its exit state; steps done by
agents name the agent; steps awaiting a human say so. A step that isn't in
the record didn't happen — the record is append-only and travels with the
package.
| Findings report | Reviewer → practitioner, Author | Per finding: severity, checklist ref, location quote, consequence, concrete fix; overall verdict |
| Review evidence pack | Analyst → Reviewer | Charts with phase lines and confound annotations; data-quality caveats first |

## Example Activation

```text
Activate NDIS Case Evidence Orchestrator.

Participant code: P-114 (de-identified — no names, DOB or NDIS numbers).
Downstream document: comprehensive behaviour support plan (an interim
exists; its 6-month clock expires in 9 weeks).
Record systems available: CRM export (12 object extracts attached) and
the participant folder listing (41 files, 3 flagged as image-only scans).

Produce:
1. Record census — per-object counts, anomalies named
2. Document manifest with read status; OCR queue for the scans
3. Evidence ledger for the comprehensive-plan fact set
4. Conflict list and searched-absence trails
5. CRM data-quality flags (empty fields whose facts were found elsewhere)
```

Then hand the ledger down the chain, activating each agent with the prior artifact and only the new facts it needs.

## Quality Bar

- No agent drafts from an unswept record — the census and manifest exist first
- Every clinical claim in every artifact traces to a ledger entry or named source
- Missing information is written as missing (with its search trail), never inferred
- Every regulated restrictive practice is named, classified and register-tracked; euphemisms do not survive the Reviewer's sweep
- Statutory timeframes are computed from record dates and verified against current guidance, not recalled
- Identified data is coded on arrival; identifiers appear in no artifact
- The package agrees with itself: plan, register, measurement and correspondence all cite the same ledger

## Boundaries This Workflow Keeps

Three are deliberate and worth knowing in advance. **Agents never
hand-format final documents**: content is the agents' work, but branding,
layout and template application belong to a single renderer (the
organisation's formatting skill or document pipeline), because formatting is
mechanical and consistency across a caseload only survives when exactly one
thing does it. Next, **the restraint-judgement fields are author-only**: the RP Officer scaffolds the full authorisation pack — sourced facts, contexts, monitoring, and the authorisation state as it stands today — because writing the pack that goes *to* the authorisation body is preparation, not authorisation, and refusing to draft it inverts the order of the process. But the four fields that justify restraining a person (least-restrictive justification, proportionality, fade-out, expected outcomes) are laid out as prompts and written only by the accountable practitioner — the same line as the function statement and the falsifier. Finally, **no agent lodges, submits or files anything**: portal submissions, Commission lodgement and record-system writes are human acts with a named human accountable for them.

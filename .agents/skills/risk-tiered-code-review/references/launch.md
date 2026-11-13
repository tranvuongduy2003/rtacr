# Launch assessment

Assess the complete release candidate in its target environment, including relevant merged PRs, configuration, and migration order. A PR readiness report is only one input. Identify the candidate revision or artifact, intended audience, owner, and approvals required by release policy. If there is no production or distribution effect, use **NOT APPLICABLE**.

Review the integrated user or operator journey against the spec. Check relevant error states, permissions, data correctness, accessibility, and performance under representative conditions. Confirm who conducted the whole-feature audit and which candidate they tested.

For a staged rollout, verify:

- **Control:** Starting audience, stage sizes, dwell times, gate or deployment control, and who may advance, pause, or revert.
- **Observation:** Baseline, metrics and dashboards, and explicit advance, stop, and rollback thresholds. Match signals to the actual risks, including silent failure or data corruption.
- **Recovery:** A tested disable, redeploy, restore, or forward-recovery procedure covering side effects and migrations; owner and expected recovery time. A flag cannot undo work already performed.

If a staged rollout does not fit, verify a proportionate release control and recovery path. A small reversible change can use routine release checks and a known rollback; a one-way change needs verified containment or recovery and explicit release-owner sign-off. Do not invent thresholds or approvals.

Report **READY** only for the named candidate and next stage with required integration checks, controls, and owner sign-offs verified. Use **BLOCKED** for a candidate with a failed or known unmet requirement, including an unresolved blocker in a change known to be part of that candidate. If candidate membership is unknown, report **UNVERIFIED** and explain any conditional blockers. Use **UNVERIFIED** as well when material evidence or approval state is unavailable. A ready verdict at one stage does not authorize promotion to the next.

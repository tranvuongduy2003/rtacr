# Risk rubric

Score the reviewed change as a whole. In each row take the highest applicable value once; add the five values. Scores measure impact, not evidence completeness. Use the higher plausible value and identify the specific unknown when impact is unclear. Ignore author risk labels, diff size, and AI attribution.

| Factor | Values |
| --- | --- |
| Surface | **0** no runtime or operational effect; **5** isolated feature or component; **15** shared module or multiple callers; **25** core entry point, shared infrastructure, or global runtime config; **30** core auth, money movement, or security control. |
| Data and privilege | **0** no data or access impact; **10** non-sensitive data, config, or telemetry; **20** personal data, user content, or session data; **25** credentials, payment data, or a change to access privileges. Score changes to handling, not data merely present nearby. |
| Reversibility | **0** no persistent effect and no runtime rollback needed, or verified containment reverses all effects; **5** ordinary code revert or redeploy restores behavior without persistent damage; **15** recovery needs manual repair, data reconciliation, or downtime; **20** effects are destructive, irreversible (including disclosure), or safe recovery for persistent effects is unproven. |
| Contracts | **0** no changed interface or compatibility obligation; **5** compatible internal change; **10** changed cross-component behavior, additive public contract, or version coordination; **15** breaking public or cross-service contract, or schema migration. |
| Exposure | **0** no runtime effect, or verified containment below; **10** runtime or operational effects without verified containment. |

Score bands: **R0** 0–9 · **R1** 10–29 · **R2** 30–59 · **R3** 60–100. Use the highest of the score band and all applicable floors:

- **R1** for any runtime behavior change, including a gated leaf, or test changes that weaken meaningful regression coverage without changing mandatory release enforcement.
- **R2** when a behavior change crosses a shared runtime boundary, affects multiple consumers, introduces a production dependency, changes a public contract, or runs a migration with verified recovery.
- **R3** for changes to authentication, authorization, sessions, money movement, secrets, cryptographic controls, production deployment or access controls, mandatory approval/CI enforcement, breaking public contracts, bulk sensitive-data handling, or destructive migrations and migrations without verified recovery. Apply floors to actual behavior and controls, not file names or incidental mentions.

**Verified containment:** Credit a flag only with evidence that it defaults off for the affected environment, has zero exposure before rollout, covers every relevant path and side effect, and that disabling it restores safe behavior. Establish ownership and cleanup for temporary flags. For an equivalent control, verify the audience boundary, effective off state, and reversal as well. A designation in the diff alone does not prove effective state or behavior. A gate does not contain migrations, jobs, or writes that run outside it, or undo persistent damage. Keep hard floors even when a change is gated.

**Related changes:** For dependent PRs that jointly implement one behavior, evaluate the combined surface and use the higher of the individual and combined tiers for routing. Record the relationship and revisions; flag a missing related diff if it prevents a readiness decision.

## Default routing

These are the skill’s review defaults for merge assessments; honor stricter repository policy as well. Name the applicable code owners or maintained team roles. If no owner is mapped, route shared and critical changes to a maintainer to identify the responsible owner. Do not lower the computed risk based on an author label or acceptance of a finding.

| Tier | Depth and required independence |
| --- | --- |
| R0 · Non-runtime | Focused diff and applicable repository checks. Confirm that documentation, formatting, or tests do not change production behavior or weaken an important check. No extra reviewer beyond repository policy. |
| R1 · Isolated | Inspect behavior, affected tests, and the limits of containment. Obtain one independent reviewer (human or fresh agent), plus any human approvals required by repository policy. |
| R2 · Shared | Deep review of callers, compatibility, affected checks, and failure recovery. Route to the responsible human owner and an additional independent human reviewer. |
| R3 · Critical | Deep review of affected boundaries, invariants, persistent effects, and safe recovery. Route to at least two independent human reviewers, including the owner and an appropriate specialist (such as security, data, or release); one person cannot count twice. |

If asked about automatic merge, report eligibility only under existing repository policy and verified conditions. The skill never recommends automatic merge for R2 or R3 and never initiates it for any tier.

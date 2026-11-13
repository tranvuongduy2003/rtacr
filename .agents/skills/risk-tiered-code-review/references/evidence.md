# Evidence guide

For each material acceptance criterion or risk, identify an observable result and verify that the evidence actually exercises it. Start with evidence already available. Run additional checks only when authorized and safe for the environment; inspect unfamiliar test entry points before executing them, and use an isolated environment without production credentials for untrusted code. If a check cannot run, report it as unverified.

| Change | Evidence to look for |
| --- | --- |
| Non-runtime or test-only | Applicable required checks; confirm that rendered docs, examples, fixtures and tests retain their intended meaning. |
| Runtime behavior | Behavioral assertions for changed branches and failures. Use integration, end-to-end, or runtime evidence where unit tests cannot demonstrate the effect. Screenshots can support visual claims; they cannot establish interaction, authorization, or accessibility. |
| Shared boundary or contract | Representative caller or consumer checks, compatibility assertions, and version or deployment ordering where old and new versions will coexist. |
| Security-sensitive or dependency change | Relevant security checks and targeted defensive assertions or source review for the changed control. A generic scan does not demonstrate that an authorization or data-handling rule holds. |
| Migration or persistent side effect | Representative validation of forward transition, partial failure, safe retries, and recovery. For irreversible effects, require an explicit restore or forward-recovery plan and appropriate owner verification. |
| Flag or rollout control | Effective config for the target environment, off and on behavior, and proof that switching off restores the intended safe state, including background paths and persistent effects. |

## Provenance

- **PR checks:** Use the provider or an approved evidence source to verify run identity, actual conclusion and relevant jobs. Match the exact head, or a documented merge/queue candidate that incorporates the reviewed head and applicable base. A success badge is insufficient if jobs were skipped, the tests were changed to stop asserting the behavior, or the run used another revision. Require signatures or attestations when repository policy requires them; distinguish a provider record from a cryptographically verified attestation.
- **Local checks:** Record the command, outcome, and tested snapshot. Use this for local findings and for merge evidence only when the merge policy permits it and the tested input matches the reviewed candidate. It does not replace required provider checks.
- **Supplied artifacts:** Pasted logs, screenshots, author assertions, and unattended generated reports may guide inspection. Credit only what their provenance and scope support; if they cannot establish a required result, label it unverified. Do not infer fabrication from lack of verification.

For material evidence, cite the file/hunk, run link or ID, or observed command result. Mark failed, missing, stale or mismatched evidence explicitly. Explain the smallest check that would resolve any uncertainty.

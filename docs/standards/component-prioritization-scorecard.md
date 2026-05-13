# Component Prioritization Scorecard (Must Haves vs Nice to Haves)

This standard defines a lightweight way to score planned components and proposals so the portfolio can stay focused during early foundation work.

## How to Use

1. For each component/proposal, answer the 13 questions below with a **1–5 score**.
2. Record the scores in the component’s PRD (or in a Splits appendix) so the decision is reviewable.
3. Classify the work:
   - **Must Have**: required to hit the current OKR key results or unblock the next stage gate.
   - **Nice to Have**: not required for the current OKR/stage; order by utility vs cost/risk.

## Scoring Scale (1–5)

- **1**: low / weak / unclear
- **3**: medium / acceptable / partially addressed
- **5**: high / strong / clearly addressed

## The 13 Questions

1. **Core KR alignment**: does this directly advance a current OKR key result?
2. **User value**: does this materially improve the end-user experience?
3. **Portfolio leverage**: does it benefit multiple repos/surfaces (NeXeZ + NuMuN + extension)?
4. **Integration risk**: does it reduce cross-repo integration failure risk?
5. **Operational risk**: does it reduce incident/release risk or improve rollback safety?
6. **Security impact**: does it strengthen authz/safety boundaries or reduce exposure?
7. **Reliability impact**: does it improve correctness (replay, idempotency, ordering, dedupe)?
8. **Accessibility impact**: does it preserve meaning in reduced-motion/high-contrast modes?
9. **Buildability**: can it be built and verified in a short, reviewable vertical slice?
10. **Testability**: can it be validated with clear checks (contract compatibility, examples, replay flows)?
11. **Complexity / effort**: how hard is it to implement? (score 5 = low effort)
12. **Time-to-demo**: does it produce a demonstrable milestone quickly?
13. **Economic value vs opportunity cost**: does it justify itself versus what it displaces?

## Ordering Nice to Haves

For Nice to Haves, prioritize by:

- high user value + high leverage + low effort,
- then by reducing operational/security risk,
- while keeping the live user website experience stable (avoid destabilizing experiments during active usage).


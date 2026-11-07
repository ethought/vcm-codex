# Architecture review package

Revision 0.22 — 7 November 2026 — **G1 passed; G2 in progress and not passed.**

[The electrical baseline](../design.md) remains the source of truth. Revision 0.14 records independent DC grid bias and the linked-setting option. [Revision 0.13](../records/design-baseline-v0.13.md), [revision 0.12](../records/design-baseline-v0.12.md), [revision 0.11](../records/design-baseline-v0.11.md), [revision 0.10](../records/design-baseline-v0.10.md), [revision 0.9](../records/design-baseline-v0.9.md), [revision 0.8](../records/design-baseline-v0.8.md), [revision 0.7](../records/design-baseline-v0.7.md), [revision 0.6](../records/design-baseline-v0.6.md), [revision 0.5](../records/design-baseline-v0.5.md), [revision 0.4](../records/design-baseline-v0.4.md), [revision 0.3](../records/design-baseline-v0.3.md), [revision 0.2](../records/design-baseline-v0.2.md) and [original revision 0.1](../records/design-baseline-v0.1.md) are archived. This package extracts its requirements, records the work request and subsequent confirmations, and proposes architecture work for review. Calculated examples establish arithmetic consistency only; they do not establish hardware performance or safety.

Read in this order:

1. [Requirements, decisions, and reconciliation findings](01-requirements-and-decisions.md)
2. [Power allocation, mains input, and thermal worksheet](02-power-allocation.md)
3. [Safety states, isolation architecture, and fault responses](03-safety-architecture.md)
4. [Board interface-control document](04-interfaces.md)
5. [Risk register](05-risk-register.md)
6. [Staged schematic and prototype plan](06-staged-plan.md)

Supporting records: [G1 decisions](g1-decisions.md), [G1 closure review](g1-closure-review.md), [G2 decisions](g2-decisions.md), [gate reviews](gate-reviews.md), [uncertainty and calibration](measurement-plan.md), [sources and tool readiness](sources-and-tools.md), [change log](../CHANGELOG.md), and [reproducible arithmetic](../analysis/power_budget.py).

## Review status

| Gate | State | Evidence available | Release condition |
|---|---|---|---|
| G1 Requirements reconciliation | **Passed 6 November 2026**, G1-09 | G1-01 through G1-08 and full tracker/verification-plan package accepted by the user | Met for requirement coverage and planned verification; unresolved engineering items retain owners and downstream gates |
| G2 Power / mains / thermal | **In progress; not passed** | Coupled rail limits, scenarios, loss model, heat ledger; G2-01–G2-06 Agreed; G2-07 internal preference recorded with placement Provisional; G2-08 simultaneous voltage target confirmed as Provisional; G2-09 simultaneous preferred with sequential option Agreed; G2-10 shared power allocation Agreed; G2-11 two active sections Agreed; G2-12 independent and linked grid-bias settings Agreed. G2-13 anode control Open | Confirm simultaneous allocation, measurement definition, duty, grid behavior, mains and heat envelopes |
| G3 Safety / isolation | Not entered; concept prepared | States, boundary matrix, fault cases | Independent safety review accepts architecture and numeric acceptance limits |
| G4 Board partition / interfaces | Not entered; logical ICD prepared | Functional cross-board links and safe defaults; physical details explicitly open | All required electrical, timing and physical interface fields closed and reviewed |
| G5 Risk prototypes | Planned only | Five prototype contracts, including microphonics, and metrology plan | G1–G4 reviewed; relevant decisions closed; prototype evidence meets each contract |
| G6 First valve path | Planned only | Recommended small-signal triode path | Repeatable complete test, calibration evidence and demonstrated protections |
| G7 Expansion | Planned only | Incremental rail, socket and test sequence | Prior gate passed; each addition repeats affected reviews and checks |

Preparing a later gate's review material does not pass an earlier gate. Detailed component selection, schematic implementation, PCB placement and routing have not started. This stopping point follows the user's explicit instruction to review the first four deliverables before those activities.

## G2 allocation review — 7 November 2026

- G2-12 agrees independent DC grid bias and the linked-setting option for both sections. R020, I012 and the measurement plan cover separate requests, readbacks and validity checks.
- G2-13 asks whether simultaneous comparison needs independent anode voltages. The recommendation is one requested anode-to-cathode voltage for both sections, with measurements and protection for each path.
- **Risks/assumptions:** concurrent paths add shared-supply/reference coupling, channel timing/attribution and fault-propagation work. Low-power use is expected by the user; representative full-profile budgets still need verification. Independent reviewer/test-operator appointments, numerical limits and other downstream decisions remain Open.
- **Current gate:** G2 power/mains/thermal reconciliation, one decision at a time. The 120 W ceiling and electrode limits remain Provisional. Detailed component/schematic/PCB work remains gated by the existing review requirements.

## Initial package session report — revision 0.1

- **Completed:** six requested draft artifacts; source-linked reconciliation; reproducible arithmetic; uncertainty/calibration framework; gate and manufacturing workflow records. Required skill files and command entry points located. No baseline requirement was promoted or retired.
- **Decisions needed for the next gate:** approve the G1 extraction and nominate accountable reviewers. To close G2 afterward, resolve D001–D008 and the power implications of D009/D018. Recommended allocation policy is to reject infeasible requests before energizing and reserve power locally; it remains open.
- **Risks/assumptions:** the individual heater/anode/screen caps total 165 W before grid power; 120 W has no confirmed averaging window or tolerance allowance; heater common-mode limits and grid source/sink behavior are unspecified; no complete safety standard review or prototype measurements have been performed.
- **Next gate:** review G1. Pass when every extracted requirement has an accepted status, source, accountable owner and verification method, and every unresolved conflict is linked to an open decision. G2 cannot pass merely because illustrative scenarios fit 120 W.

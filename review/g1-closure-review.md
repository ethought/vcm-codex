# G1 closure review

6 November 2026 — **Accepted under G1-09; G1 passed.**

Accepted review basis: [archived baseline revision 0.2](../records/design-baseline-v0.2.md), tracker revision 0.9 ([current tracker](01-requirements-and-decisions.md)), [confirmed G1-01 through G1-08 decisions](g1-decisions.md), the archived work request and change log. G1-09 closes requirements reconciliation only; accepted revision hashes are retained in [gate reviews](gate-reviews.md).

## Confirmed interpretations

| Item | Confirmed disposition |
|---|---|
| Test coverage | Presented baseline test list is Agreed scope; detailed limits remain Open/Provisional |
| Heater | 0–50 V, 60 W, approximately 8 A at low voltage remain Agreed coupled capability requirements; waveform/noise/float/duty/allocation Open |
| Electrode/combined power | Anode, screen, grid and 120 W combined ceiling remain Provisional pending G2 |
| Precision | All four targets remain Provisional while definitions and supporting evidence are developed |
| Rectifier allocation | Detailed allocation Open; main-unit tests Agreed; full-load fixture Deferred/separate; optional PIV fixture Provisional/separate, both excluded from main-unit budget |
| Microphonics | Agreed inclusion under corrected G1-06 instruction; implementation D022 Open; baseline revised with original archived |
| Physical boards | Provisional until safety/interface review; no one-PCB-per-module requirement |
| Ownership | User accountable across U/E/M/F; Codex prepares engineering work/checks; user appoints independent S reviewer before G3 sign-off |

## Coverage and planned verification

| Requirement group | IDs | Verification planning carried into later gates |
|---|---|---|
| Product/control/adapters and scope boundaries | R001–R010 | API/control/disconnect tests; adapter validation; scope and separate-fixture review |
| Electrical/audio/microphonics coverage | R011–R025 | Reference loads, known faults, repeated valve tests, controlled stimulus/response checks and defined waveform/operating conditions |
| Heater, electrodes, combined power and heat | R026–R039 | Coupled envelopes; worst simultaneous/line/load/duty cases; hardware-limit, transient and thermal tests |
| Precision and calibration | R040–R048 | Range-specific uncertainty budgets; independent standards; as-found/as-left and validation points |
| Safety and physical layout constraints | R049–R060 | Independent boundary/state/fault review; local protection tests; verified discharge and access; return/noise analysis |
| Proposed modules and interfaces | R061–R070 | G3/G4 partition/ICD completeness, failed-interface and isolation/reference review |
| Process, prototype, routing and manufacturing controls | R071–R080 | Ordered gate records, prototype contracts, skill workflows, ERC/DRC and manufacturing evidence at relevant releases |

Every tracker requirement has a unique ID, status, rationale/source, accountable role mapping/decision needed and planned verification method. At G1 acceptance there were 80 requirements and 22 detailed decisions: D019 inclusion was Agreed and 21 detailed decisions were Open. Those Open decisions had owners and downstream gate/evidence needs. Subsequent status changes are recorded in the current tracker and [G2 decisions](g2-decisions.md). The 20 reconciliation findings remain visible; accepting G1 does not erase them.

The verification column states **what must be checked**, not a completed test or a complete numeric acceptance contract. Before the relevant prototype/design release, the named decisions must supply numerical limits, conditions, equipment, procedure, fault cases and responsible tester/reviewer. A missing technical limit cannot be treated as a test pass.

## Owned work that remains after G1

| Work | Accountable owner / next evidence gate |
|---|---|
| Simultaneous power, grid behavior, duty, mains and thermal/load-bank envelope | User U/E/M, with Codex preparation; G2, D001–D008 plus D009/D018/D021/D022 implications |
| Safety design basis, independent reviewer appointment, isolation and numeric fault/discharge/access criteria | User owns resolution/appointment; appointed S provides independent review; G3, principally D009/D011–D015 |
| Detailed ranges/uncertainty/calibration, transport, matrix and physical interface definitions | User U/E/M/F, with Codex preparation and S review where applicable; G4/G5, D010–D018/D021/D022 |
| Microphonics stimulus/fixture/measurement implementation | User U/E/M, with S involvement for guard/fault behavior; D022 across G2–G5 and the accepted integration stage |
| Physical test execution, reference instruments and raw evidence | User arranges actual tester/resources when each test plan is released; G5 onward |
| Separate full-load/PIV fixture operating conditions and detailed goal allocation | User U/E with independent S review; D020 and separate fixture gates; no main-unit budget inclusion |

The reviewer identity is still Open, but responsibility for appointment is assigned. It is a required action before G3 sign-off; G1 acceptance does not waive it.

## Accepted disposition

**Pass G1**, accepted by the user on 6 November 2026, for tracker coverage and the planned verification approach. G2 is now in progress for power/mains/thermal reconciliation using the Provisional ceiling and electrode inputs. This does not approve G2 itself, validate any circuit, or release detailed component selection, schematic or PCB work before the existing first-four-deliverables reviews and relevant decision closures.

User G1-09 disposition: **pass**. Gate pass date: **6 November 2026**. Requirement statuses and limits are unchanged. See [G1-09](g1-decisions.md#g1-09--requirements-reconciliation-and-verification-plan-acceptance) for the exact confirmation and [session verification](session-verification.md) for document checks and their limits.

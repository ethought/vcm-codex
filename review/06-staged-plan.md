# Staged schematic and prototype plan

Revision 0.6 — 7 November 2026 — planning only; microphonics, fan cooling and G2-07 preferred internal-bank and G2-09 comparison-mode and G2-11 two-section implications included; no schematic, parts or PCB selected.

Trace: R071–R080; D017,D018. Proceed G1→G2→G3→G4→G5→G6→G7. Later-gate draft documents do not authorize implementation. Once the **first four deliverables are reviewed** and relevant product/safety decisions resolved, finalize physical connector choices and the ICD; then close G4 before detailed functional schematic capture. This separates review of the logical interface contract from its final physical release without requiring premature connector selection.

## Schematic sequence after review

| Stage | Schematic scope to prepare | Entry condition | Exit evidence / pass condition |
|---|---|---|---|
| S0 | Independent safety chain, low-voltage control, logging and simulated module interfaces | G1–G4 release, numeric permit/timing contract | All state transitions/fault inputs demonstrated with bounded dummy interfaces; MCU/PC cannot override inhibit |
| S1 | Protected precision V/I path, self-check and external-calibration interface | D010/D011/D016 closed for initial ranges | P-M evidence; no raw HV exposure at calibration port; independent reference comparison |
| S2 | Limited-energy heater/reference and matrix coupons | D008/D009/D012/D014 closed for tested subset | P-H/P-X contracts met; no uncontrolled common mode or energized commanded rerouting |
| S3 | One current/energy-limited anode channel, negative grid bias and independent cutoff/discharge | G3 fault limits and prototype setup independently reviewed; S0 infrastructure ready | P-E contract met over initial envelope; loss of bias/control/mains demonstrated |
| S4 | First complete triode path: PC → local safety → supplies → matrix → socket → measurement → log | Relevant P-H/P-X/P-E/P-M evidence accepted; D017 confirmed | G6 end-to-end contract below; repeatable valid data with all protections demonstrated |
| S5 | Extended voltage/current, screen, positive-grid/source-sink operation | G6 passed; update G2/G3/G4 for each extension | Full rail and simultaneous-limit/thermal validation, cross-rail sequencing and faults |
| S6 | AC/DHT operation, further bases, leakage ranges, amplifier/rectifier coverage | Earlier stage passed for dependencies; coverage decisions confirmed | Each new test has uncertainty, load, thermal, matrix and protection evidence |
| Separate | Full-load 5U4GB and optional ~1,550 V PIV fixtures | Explicit new fixture scope/safety/power reviews | Separate gate records and manufacturing packages; no main-unit budget borrowing |

## Risk-reduction prototype contracts

G1-06 includes microphonics/tap testing in the current architecture scope. D022 must resolve stimulus method, electrical/mechanical interfaces and measurement criteria before the affected design is released. Its build/integration position remains Open; the first triode path is not assumed to validate it. Any powered stimulus adds a G2 auxiliary/thermal budget item and G3 guard/fault obligations. The agreed capability is not Deferred to G7.

G2-06's preferred fan-assisted cooling (R082) adds explicit checks within the existing five contracts: P-E covers continuous heat at the R081 ambient endpoints, loss of required cooling and thermal-control faults; P-M covers fan/control electrical interference and temperature-related measurement changes; P-T covers cooling-related vibration/background artifacts across approved fan states. Numeric noise, fault and thermal criteria remain Open before these contracts can be released. No fan-off test mode or cooling hardware is selected, and no prototype gate is passed by this planning update.

G2-07 prefers the resistive bank internally, with final placement Provisional. Extend P-E thermal/fault planning and P-M/P-T measurement checks to the shared-enclosure heat and fan interaction, using R081 ambient and reviewed load conditions. A single-channel coupon or the low-power first valve path cannot validate the full enclosure's continuous heat budget; integrated thermal evidence is required before releasing the larger envelope. No resistor or enclosure geometry is selected.

G2-09 agrees simultaneous pair/section comparison as preferred, with sequential mode available. S3/S4 and the first one-section path remain staged experiments; they do not establish full product comparison coverage. G2-11 sets the required concurrent capacity to two sections. Include a two-path integration increment after its dependencies are met, with placement in the sequence still to be reviewed. Verify both sections of one dual-section valve and two single-section valves, plus the two-pass procedure for a pair of dual-section valves; actual valve/base/profile choices remain Open. Extend P-E/P-H/P-X to shared-budget reservations, heater/reference combinations, cross-channel faults/backfeed and safe mode transitions, and P-M to channel attribution, timing/skew, crosstalk and simultaneous-versus-sequential repeatability. Use representative low-power pairs plus worst approved asymmetric loading. Release of this capability requires both modes to meet reviewed limits; no simultaneous capability is Deferred by keeping the first prototype small.

All numeric thresholds, duty and test instrumentation must be entered and reviewed **before** energization. A contract containing TBD values is not a pass. Start with dummy loads and low stored energy, then increase stress only within the independently reviewed test plan. Actual component selection begins only after the first four deliverables' review.

| ID | Experiment / hypotheses | Required operating and fault tests | Explicit pass evidence |
|---|---|---|---|
| P-H | Floating AC/DC heater/reference can meet differential, common-mode and noise requirements without corrupting DHT measurement | Envelope corners including ~8 A region and 50 V/1.2 A; cold inrush; AC RMS/peaks/harmonics; DC ripple; allowed positive/negative float; reference changes only discharged; H–K short/open reference/sense loss; PC/interlock/control-power loss | Every accepted V/I/P tuple within approved regulation/noise/thermal bounds; all fault energies/times below G3 limits; correct measured split of filament and cathode currents; safe discharge under loss of control |
| P-E | One electrode path can regulate quietly and shut down independently over its approved envelope | Initial reduced envelope, then validated extension; line/load transients, short/no load, dropout heat, overshoot, sensor faults, bias/anode dependency, stuck pass element, fan loss, retained charge and repeated discharge | Measured SOA/temperature margins, transient energy, ripple and settling satisfy limits; independent cutoff works with controller halted; every storage node meets discharge/access contract |
| P-M | Entire measurement path meets uncertainty and rejection goals | Zero and multi-point standards per range/polarity; range overlap; overload recovery; source impedance; temperature/time drift; common mode and switching noise; leakage contamination; calibration reference faults; source/analyzer loopback | Complete populated uncertainty budget, as-found/as-left and independent validation data; guard-banded error within approved specification at all points; no false valid data on saturation or broken sense |
| P-X | Matrix supports intended maps with acceptable leakage/capacitance/contact heating and safe fault behavior | Allowed/forbidden connectivity; contact weld/open and power-loss dropout; socket-side trapped charge; adjacent-rail stress; low-level leakage; full heater current later; wrong adapter and interrupted reconfiguration | No unintended energized connection; readback detects tested faults; routing blocked above approved residual threshold; insulation and thermal/noise limits met; pin-to-terminal mapping audited |
| P-T | Controlled microphonics test produces repeatable, attributable response data | Chosen stimulus method/location/level and valve operating point; no-stimulus controls; repeated events and re-mounting; response bandwidth/window; actuator/sensor faults if present; loss of link/interlock and aborted stimulus; guarded fixture integrity | Approved numeric stimulus/response repeatability and scoring criteria met; valid stimulus metadata accompanies each result; noise/fixture artifacts characterized; every applicable fault obeys G3 limits; no access or isolation bypass |

Measure normal operation, startup, shutdown, communications loss, interlock opening, overload, short and single-fault behavior for **each** circuit; the [ICD](04-interfaces.md) supplies the starting per-module contract. Preserve raw traces and instrument setup, not just a “pass” sentence.

## Recommended first end-to-end valve path — Open D017

Use one indirectly heated small-signal triode section, with one adapter and a deliberately small permitted routing subset. A candidate is **one section of an ECC82/12AU7**. Its manufacturer's sheet specifies 6.3 V/300 mA or 12.6 V/150 mA heater operation and identifies it as a double triode. Exact manufacturer variant, physical pin map and operating point still need approval. The candidate is a test article, not a selected electronics BOM component. [JJ Electronic ECC82 datasheet, p.1](https://www.jj-electronic.com/images/stories/product/preamplifying_tubes/pdf/ecc82.pdf).

Proposed initial envelope for review: DC heater 6.3 V nominal (1.89 W nominal heater power), anode **no more than 100 V and 5 mA** (0.5 W delivered bound), non-positive grid bias chosen from the accepted valve's curves, screen disabled, unused triode section treated according to the verified profile. The 100 V/5 mA limits are conservative **engineering proposals**, not a quoted datasheet operating point or a safe-touch voltage. Exact setpoint, current range, grid cutoff range, cathode reference, warmup duration and dissipation limits are TBD. Neither all valves nor all biases will draw 5 mA at 100 V. A 1 W grid reservation in the power worksheet is a placeholder, not predicted consumption.

Recommended sequence:

1. Simulated PC request and dummy load verify the entire command/result/fault path before a valve is installed.
2. With energy disabled and discharge independently verified, identify the adapter, verify its pin map electrically and establish the selected cathode/heater reference. Demonstrate an invalid map is rejected.
3. Close/secure the guard, perform approved bounded cold continuity/short checks, discharge again, and revalidate the static map before heater enable.
4. Ramp heater under local limits; confirm current, voltage and warmup stability. Establish safe non-positive grid bias before ramping anode; screen remains inhibited locally.
5. Acquire a static operating point and a small approved grid-step pair for a first transconductance estimate. Log actual terminal voltages/currents, timestamps, profile/map revision, calibration identity and validity flags. A provisional estimate is not a ±1% claim.
6. Execute normal shutdown, measured discharge and access release. Repeat with PC cable loss, interlock loss, bias fault, output short in a safe dummy fixture and control-power interruption.

This path exercises pin routing, heater, anode, grid, precision current/voltage, local safety and logging with a small delivered-energy budget. It does not establish AC/DHT, screen, full-voltage, power-valve or analyzer performance. Those are planned expansions, not silently removed capabilities.

**G6 pass contract, all fields required before build:** accepted valve/profile/map; numerical regulation/current/noise/uncertainty limits for this subset; independent reference instruments and certificates; explicit test count, repeatability criterion, ambient/warmup/duty; measured protection and discharge deadlines; evidence from every injected fault; rejection of invalid commands; no unsafe restart/reconfiguration. Actual measured values, not a manufacturer's typical curve alone, establish repeatability. Product accuracy targets remain provisional until supported.

## Layout, routing and manufacturing after successful circuit reviews

Before placement, approve the isolation/spacing and current/thermal/analog-return constraints in the [tool and manufacturing workflow](sources-and-tools.md). Use the installed **ktl-route** workflow for routing. Review every voltage domain and sensitive net role; do not derive HV constraints from names or replace the router. ERC/DRC alone cannot validate insulation, thermal behavior, analog accuracy or safe fault operation.

Each candidate board revision needs relevant ERC, full connectivity/DRC, explicit review of allowed exceptions, supply/current/temperature checks, isolation/return-path review and JLC terminal/placement audits. G5 prototype fabrication is prototype release, not production release. A board is not “ready for fabrication” until its applicable checks and exact matching manufacturing set have been reviewed.

## Review contract

**Decisions made:** no valve or prototype limits confirmed; staged scope proposed. **Open:** D017 and linked prototype contracts. **Assumption:** external reviewed isolated bench power can reduce the first prototype's mains-design work, subject to G3. **Failure modes:** all linked P-H/P-E/P-M/P-X and safety-table cases. **Verification plan:** bounded coupons → dummy integration → one valve path → increments, preserving raw evidence. **Pass for this plan:** agreed stage scope, owners/resources and filled test contracts; **G5/G6 pass requires physical results**, which do not yet exist.

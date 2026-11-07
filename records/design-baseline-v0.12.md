Vacuum-Tube Valve Tester — Electrical Design Baseline

Document status: Working baseline
Revision: 0.12
Date: 7 November 2026
Purpose: Keep the agreed product scope, provisional electrical limits, module boundaries, and unresolved design decisions in one reviewable place. This is a requirements and planning document, not a production-ready schematic.

1. Status key

Agreed: Explicitly accepted as part of the intended product.

Provisional: A working design target that still needs engineering validation.

Open: No final decision yet.

Deferred: Deliberately outside the current design stage.

2. Product intent and scope

Design a PC-dependent vacuum-tube tester with modular hardware, a programmable socket pin matrix, broad static and dynamic test coverage, high measurement precision, automatic calibration support, and local hardware protection. The PC application is required for operation and results display; the tester must retain essential protection and safe shutdown behavior without relying on the PC.

The current stage is focused on the electronic architecture and design process. Valve database structure is deferred. Output-transformer amplifier testing is excluded for now; amplifier performance tests use resistive loads. High-power rectifier tests are separate from the main unit.

3. Agreed product capabilities

3.1 Control and modularity

Agreed: PC-dependent control through a documented hardware API, with measurements streamed to the PC.

Agreed: Interchangeable socket adapters for different physical valve bases.

Agreed: Programmable pin routing within an adapter so different valves sharing a base can use different pin assignments without a new adapter for every pinout.

Agreed: The PC can request tests and configure operating points, but a local hardware safety supervisor independently enforces interlocks and shutdowns.

3.2 Test coverage

The system is intended to support:

Heater continuity and actual heater-current measurement.

Cold checks for shorts and inter-electrode insulation/leakage.

Hot leakage tests, including heater-to-cathode insulation for indirectly heated valves.

Directly heated valves, where the filament also acts as the cathode.

Emission or cathode-current capability testing.

Anode, screen, and grid-current measurements; gas/grid-current checks.

Transconductance, plate resistance, amplification factor, and static/dynamic characteristic curves.

Intermittent-fault detection during a test interval.

Agreed: Matched-pair comparison and dual-section balance with simultaneous operation as the preferred mode and a selectable sequential mode. Support concurrent operation of the compared valves or sections, with separately attributable measurements and local protection. Exact channel/socket count, independently adjustable versus shared supplies, heater arrangements, acquisition timing and comparison criteria remain open.

Diode and rectifier tests under load.

Amplifier-performance tests using resistive loads: gain, THD/harmonics, frequency response, noise and hum, two-tone intermodulation, maximum clean output, and warm-up drift.

Agreed: Include a controlled microphonics/tap test. Stimulus method, repeatability, measurement conditions, acceptance criteria, and implementation sequence remain open.

3.3 Heater system

Agreed: Heater range 0–50 V, up to 60 W, with up to approximately 8 A at low voltage.

Agreed: Both AC and low-noise DC heater modes.

Agreed: Heater outputs are isolated and floating-capable, with a selectable/programmed reference appropriate to the valve profile, including directly heated valves.

The 60 W limit constrains combinations of voltage and current; 8 A is a low-voltage capability, not available across the full 0–50 V range.

3.4 Calibration and precision

Agreed: Built-in references for routine self-checks.

Agreed: A plug-in external calibration module connects through an accessible connector so calibration can be performed without opening the enclosure; the PC guides and logs the process.

Agreed: Calibration records include date, reference/module identity, measured results, corrections, and status.

Provisional targets: Voltage accuracy ±0.1%; current accuracy ±0.5%; gain and transconductance ±1%; audio analyzer residual below 0.01% THD+N at 1 kHz.

These are design goals pending circuit analysis, prototype validation, and a defined calibration method. Internal self-check alone does not establish traceability.

4. Provisional supply and power limits

These are a starting envelope for architecture work. They are not final component ratings or verified operating limits.

Rail / function

Proposed range and limit

Status / notes

Anode

0–600 V; up to 150 mA at full voltage; up to 200 mA at lower voltage; 90 W power cap

Provisional. Voltage, current, and power limits must all apply.

Screen

0–500 V; up to 50 mA; 15 W power cap

Provisional. Power cap limits current at high screen voltage.

Grid

−150 V to +20 V; up to 50 mA peak

Provisional. Grid power and transient limits remain open.

Heater

0–50 V; 60 W; up to about 8 A at low voltage

Agreed capability target; validate waveform, regulation, floating range, and thermal behavior.

Combined main-unit outputs

120 W maximum combined output across heater and electrode supplies

Provisional working ceiling accepted for architecture planning. Enforce in hardware as well as software. Individual rail caps remain subordinate to the combined ceiling.

The earlier estimate of roughly 100 W for combined HT output is superseded by the proposed 120 W combined main-unit output ceiling. It is not a claim that every rail can reach its individual maximum simultaneously.

Agreed: Simultaneous and sequential comparison modes share the same main-unit combined output budget. Count all energized heaters and electrode/test-stimulus paths, with local reservations for the complete requested configuration. The 120 W ceiling remains provisional and is not multiplied by channel count. Changing to sequential operation requires explicit selection and revalidation; do not switch modes silently to make a profile fit. Per-channel electrode voltage/current/power envelopes, current sharing and hardware implementation remain open; adding simultaneous capability does not automatically duplicate the existing rail ratings.

Agreed allocation interpretation: Treat the 90 W anode, 15 W screen and 60 W heater capacities as main-unit totals shared across active test paths, allocated flexibly to requested profiles without a fixed equal split. The anode and screen power targets remain provisional; the heater capability intent remains agreed. Their 165 W sum cannot be used simultaneously under the provisional 120 W combined ceiling, which also includes grid and other delivered stimulus power. Per-path limits still bind; this does not guarantee that any one channel can use an entire shared capacity or select common-voltage supplies. Grid source/sink allocation, aggregate versus per-channel current limits, reservations, margins and detailed continuous/thermal evidence remain open.

Provisional: Retain simultaneous 600 V anode and 500 V screen as a design target, subject to individual rail voltage/current/power limits, the combined allocation, and valve-profile limits. Do not impose a separate mutual-exclusion rule on these voltage maxima. At the provisional 90 W anode and 15 W screen caps, currents are limited to 150 mA and 30 mA respectively; their 105 W total leaves 15 W for heater, grid and any other delivered stimulus before margins under the provisional 120 W ceiling. Approved continuous combinations, reservations, margins, thermal feasibility and protection remain open; this target does not validate hardware or insulation ratings.

Agreed: Reject a requested test profile before enabling it if its declared simultaneous operating envelope exceeds individual rail or combined power limits. Reserve power locally for the profile's bounded demand and report the conflicting limits. Do not automatically adjust the requested test settings; revised profiles require explicit selection and revalidation. Numeric reservations, averaging window, margins, transient allowances, and detailed fault behavior remain open. The 120 W ceiling and electrode limits remain provisional.

Agreed: Define the combined output-power accounting boundary at the valve/load connection terminals of the adapter/fixture, including heater and all electrode/test-stimulus power delivered into that circuit. Count each supplied contribution once, including power shared between a valve and resistive load. Budget upstream conversion, wiring and switching-matrix losses separately as input demand and heat. Controls, relays, cooling and any microphonics actuator require auxiliary input/heat budgets. The separate full-load and optional PIV fixtures remain outside the main-unit output budget. Sensor placement, exact port/reference definitions and directly heated filament accounting remain open.

Agreed: Give no returned-energy credit against the combined output allocation. Count supplied power without subtracting energy returned at any port or during other parts of the accounting window. Each absorption path requires separate continuous-power, peak/pulse-energy and thermal limits. The numerical absorption ratings, averaging window, margins and protection implementation remain open. This policy does not require or select a regenerative supply, and does not promote the provisional 120 W ceiling or electrode limits.

Agreed: Use continuous operation as the main-unit design basis at its eventual approved steady operating combinations, within defined ambient and installation conditions, without a normal-operation timeout or mandatory cooldown. Use 120 W as the provisional combined planning ceiling; numerical electrode and combined limits remain provisional. Peak-only grid capability, startup surges and other pulse modes require separate ratings. Valve, load-bank and absorption-path limits remain independently binding. Exact continuous operating combinations, cooling implementation, internal thermal limits and validation remain open.

Agreed: Support the eventual approved continuous main-unit operating envelope over 0–40 °C ambient, using 40 °C as the hot-ambient design/test condition. Ambient is the local air around the main unit, including cooling-inlet air where applicable; exact measurement placement and installation conditions remain to be specified. This defines a power/thermal operating requirement, not internal component or shutdown temperatures. Precision-target temperature, warm-up and calibration conditions remain open separately. Storage temperature, humidity/condensation, altitude and safety-environment classification remain open.

Agreed: Prefer heatsinks with temperature-controlled fan-assisted cooling for the main unit. Preserve the agreed audio, low-noise and microphonics capabilities and independent local protection. Fan-generated noise, vibration and electrical interference must be assessed. Numerical noise/vibration limits, cooling-fault limits, fan/heatsink/control hardware, airflow, power, sensor placement and other implementation details remain open. This preference does not establish thermal feasibility or require fans to run at every operating point.

The combined output ceiling is not the same as the mains input rating: conversion losses, control electronics, cooling, and other loads increase input demand. The resistive load bank can dissipate substantial power and needs a separately defined rating and thermal design.

Provisional: Prefer an internal main-unit resistive load bank and develop that option first, using the agreed temperature-controlled fan-assisted cooling approach. Final placement depends on continuous thermal feasibility at 40 °C ambient, separation from precision circuitry, measurement performance and local protection. Include resistor dissipation in enclosure heat while counting its tester-supplied power only once in the output budget. Resistance values, electrical/pulse/continuous ratings, airflow, guarding and interface details remain open. An external bank is an alternative for later review if evidence shows the internal approach cannot meet requirements; it is not the selected direction. The separate full-load/PIV rectifier fixtures remain unchanged.

4.1 Separate rectifier fixtures

Deferred/separate: A full-load 5U4GB test may require roughly 130 W of load dissipation under the contemplated conditions. Keep this out of the main unit's 120 W output budget and design it as a separately reviewed fixture.

Provisional/optional: A dedicated reverse/PIV test approaching 1,550 V for a 5U4GB. This is outside the 600 V main anode range and must remain a separate optional fixture pending safety, insulation, and product-scope review.

Rectifier test goals include per-section loaded voltage drop and balance, regulation/ripple using capacitor-input or choke-input conditions, startup surge, warm-up stability, and hot/cold leakage.

5. Proposed PCB and assembly boundaries

These are functional modules; the final number of boards may change after interface and safety review.

Module

Responsibilities

Boundary / notes

Mains entry and safety

Input protection, isolation strategy, protective earth/chassis arrangement, enclosure interlocks, emergency inhibit, discharge path

Physical and electrical separation from low-level measurement. Exact implementation requires safety engineering review.

Control, communications, and safety supervisor

PC/API link, commands, state machine, monitoring, watchdog, fault latching, safe inhibit

PC is not the sole safety controller. Local supervisor must be able to inhibit energy independently.

Heater supply

AC/DC generation, 0–50 V control, current measurement, floating reference, output isolation

Keep quiet measurement and selectable reference behavior explicit at the interface.

Electrode supplies

Anode, screen, and grid generation and measurement; independent rail limits; combined power allocation

Local voltage/current/power protection, controlled ramping, and discharge behavior.

Measurement and audio

Precision voltage/current acquisition, curve data, low-noise signal source/analyzer path, calibration switching

Separate sensitive analog paths from switching power circuitry; define ranges and grounding strategy before layout.

Pin-routing matrix and socket interface

Relay/switch routing between supplies, measurement points, and adapter pins

Default safe state; pin matrix may change only under a defined de-energized condition. Adapter carries physical socket; software/profile provides pin map and limits.

Load bank and external fixtures

Resistive amplifier loads; separate rectifier fixtures

Thermal/power handling physically distinct from precision analog board. Connectors must prevent unintended use or energization.

Calibration module

External precision standards and switching/identification as needed

Plug-in workflow; no case opening. Connector pinout and reference specifications remain open.

6. Interface rules to settle before detailed schematics

For each board-to-board interface, create a controlled table specifying:

Connector identity, pin numbering, keying, and mating part.

Signal name, direction, electrical range, accuracy/noise requirement, and reference/return.

Isolation domain and allowed common-mode/floating voltage.

Power source, maximum current, and fault behavior.

Enable, inhibit, interlock, and fault signals, including default state if disconnected.

Startup/shutdown sequence and whether connection or relay switching is allowed while energized.

What is monitored locally versus by the PC.

Do not assign connector pinouts, insulation distances, or protection part numbers until the isolation architecture, enclosure, intended use, and applicable safety review are established.

7. Safety behavior requirements

High voltage must default off at power-up, reset, communications loss, watchdog timeout, open interlock, or detected fault.

Local hardware must enforce overcurrent/overpower shutdown and inhibit unsafe switching independently of PC software.

Define controlled ramp-up, test completion, fault shutdown, and automatic discharge states; confirm discharge before allowing access or changing socket routing.

Validate the valve profile and selected pin map against rail limits before enabling outputs. Unknown or conflicting configuration must fail safe.

Record fault cause and relevant measured values for review.

Safety state machine and thresholds must be reviewed before detailed high-voltage implementation.

8. Design gates and verification plan

Each gate has a written pass condition and a record in the requirements tracker.

Requirements baseline: Reconcile all agreed, provisional, and open items. Pass when every requirement has an owner/status and a planned verification method.

System power and thermal envelope: Decide allowed simultaneous rail loading, mains input target, losses, cooling, and load-bank dissipation. Pass when worst-case conditions are defined and plausible.

Safety architecture: Document operating states, interlocks, fault response, discharge, isolation domains, and safe defaults. Pass after independent design review.

Board interfaces: Publish connector and signal/interface tables before detailed schematics. Pass when every cross-board connection has levels, references, limits, and failure behavior.

Risk prototypes: Test the highest-risk functions separately: floating heater (AC and DC), one electrode-supply channel, precision voltage/current path, and pin-routing matrix. Pass against predefined limits and fault cases.

First end-to-end valve path: Build one low-risk supported valve path from PC command through supply, socket, measurement, and result logging. Pass when a repeatable test can run with protections demonstrated.

Expansion: Add further rails, sockets, and tests only after the preceding gate passes; retain measured evidence and update the tracker.

9. Open decisions before detailed schematic capture

Exact admitted simultaneous operating combinations and per-channel envelopes within the shared 90 W anode, 15 W screen and 60 W heater capacities and the 120 W combined ceiling; current sharing, grid allocation, reservations, margins and validation remain open.

Channel/socket count, independently adjustable versus shared supplies, heater sharing, acquisition timing, comparison criteria and mode transitions for the agreed simultaneous and selectable sequential comparison modes.

Grid power/transient limit and exact per-electrode current ranges and measurement ranges.

Engineering validation and exact continuous operating combinations for the provisional simultaneous 600 V anode / 500 V screen target, including current allocation, margins and thermal limits.

Mains input rating, overall efficiency target, enclosure, cooling, and thermal shutdown thresholds.

Load-bank resistance choices, power ratings, duty cycle, cooling, and feasibility of the preferred internal placement.

AC heater waveform/frequency and accuracy; DC ripple/noise target; allowable heater-to-cathode common-mode/floating range.

Measurement ranges, bandwidth, resolution, uncertainty budget, sampling rates, and calibration points.

Socket-matrix switching technology, safe-state definition, and adapter identification method.

Exact API transport/protocol and behavior during PC disconnect; safety must remain local.

Calibration connector pinout, external module reference specifications, and calibration interval policy.

Microphonics/tap-test stimulus method, fixture and interface requirements, repeatability, measurement conditions, acceptance criteria, and implementation sequence.

Scope and safety review for the separate 5U4GB load and optional 1,550 V PIV fixtures.

10. Working design rule

Do not begin a full schematic or PCB layout until the relevant gate is passed. When a value is not yet established, label it provisional or open, state what evidence would resolve it, and avoid silently turning an estimate into a requirement.

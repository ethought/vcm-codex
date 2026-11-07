# Power-allocation worksheet

Revision 0.15 — 7 November 2026 — G2 review in progress after G1-09 acceptance, **not an approved operating envelope**; G1-06 microphonics scope included.

Trace: R026–R039, R050, R068; D001–D009,D018,D021. The 120 W ceiling and electrode limits remain Provisional. Heater capability intent remains Agreed; its waveform, thermal and simultaneous-use envelope remain unresolved.

[G2-01](g2-decisions.md) confirms D001 request/allocation policy: reject infeasible profiles, reserve power locally, and require explicit revised settings. G2-02 agrees the valve/load-terminal accounting boundary and separate loss/auxiliary budgets. G2-03 agrees no returned-energy credit with separate absorption limits. G2-04 agrees continuous operation as the steady-state design basis. G2-05 agrees 0–40 °C ambient for the continuous envelope (R081). G2-06 agrees temperature-controlled fan-assisted cooling as the preferred approach (R082). G2-07 records the user's internal-first load-bank preference, with placement Provisional pending feasibility. G2-08 confirms simultaneous 600 V anode / 500 V screen as a Provisional target within individual/combined/profile limits. G2-09 agrees simultaneous comparison as preferred with selectable sequential operation under the same combined budget. G2-10 agrees shared rail power capacities with flexible allocation and unchanged numerical statuses. G2-11 agrees two active section paths. G2-12 agrees independent DC grid bias with linked equal requests. G2-13 anode control awaits review. Other worksheet proposals remain unapproved unless explicitly confirmed. G1 passed requirements reconciliation only.

## 1. Boundary and definitions to review

**Agreed accounting boundary, G2-02:** power delivered to the valve/load at the adapter/fixture connection terminals, including heater and every energized electrode/test stimulus. Count each supplied contribution once, including power shared between valve and load. Upstream conversion and wiring/matrix losses belong in the separate input/heat budgets; controls, relays, cooling and any microphonics actuator have auxiliary budgets. Exact port/reference definitions, DHT filament accounting and measurement placement remain Open under D004/D009. Separate full-load/PIV fixtures remain excluded.

For each port use instantaneous signed `p_j(t) = v_j(t) × i_j(t)` with positive power into the valve/load and a documented polarity convention. **Agreed accounting policy, G2-03:** `P_budget = Σ average(max(p_j(t), 0))` gives no credit for energy returned at any port or during other parts of the window. Track `P_return = Σ average(max(−p_j(t), 0))` separately and enforce each absorption path's continuous/peak/energy/thermal limits. Numerical ratings, exact port definitions, averaging window, uncertainty/margins and response delay remain Open. Also constrain instantaneous current, voltage and pulse energy; a 120 W average alone does not bound a short pulse.

This gross allocation is a capacity measure. Actual input/heat budgets must trace supplied and returned energy without double counting. The source-only illustrative efficiency model below has no implemented return/recovery path and cannot establish regenerative input demand or sink dissipation. No regenerative topology is selected.

For DC resistive examples, `P = V × I`. For AC, real heating power is the average of `v(t)i(t)`; `V_rms × I_rms` is apparent power and equals real power only at unity power factor. Use simultaneous sampling or a justified equivalent method, and specify crest factor, peak voltage/current and waveform. DHT filament power must exclude cathode-current contributions through the filament reference; its current-path model is still Open.

For grid power, negative voltage does not automatically mean negative delivered power: the current sign also matters. Both the sourcing and sinking quadrants need ratings. The 50 mA figure is a peak input to analysis, not permission for continuous 50 mA at either endpoint.

## 2. Voltage/current targets and shared power capacities

**G2-10 Agreed allocation interpretation:** sum sourced power across all active paths of each function: `Σ Ph,k ≤ 60 W`, `Σ Pa,k ≤ 90 W`, and `Σ Ps,k ≤ 15 W`. Anode/screen values remain Provisional; heater capability intent remains Agreed. Also enforce the Provisional 120 W combined limit including every grid/stimulus path, using the agreed no-returned-energy-credit convention. Allocate flexibly to the selected profiles, without a mandatory equal split; per-path ratings, current sharing, windows and margins remain Open.

The following table and heater-current examples illustrate the original range/power coupling for a single active path using the full relevant capacity. They do not approve that entire capacity on every channel, or simultaneously on multiple channels. For several active paths, replace the available power in each path's calculation with its admitted allocation and apply the eventual per-path/current limits as well. Existing 200 mA anode, 50 mA screen and approximately 8 A heater targets are not automatically duplicated or interpreted as accepted aggregate current limits by this power-only decision.

| Rail | Planning inequality for positive source operation | Consequence | Still unresolved |
|---|---|---|---|
| Heater | `0 ≤ Vh ≤ 50 V`; `Ih ≤ min(8 A, 60 W / Vh)` for Vh > 0 | 8 A through 7.5 V; 1.2 A at 50 V | Approximate 8 A tolerance, AC RMS meaning, inrush, minimum regulation, common-mode and noise |
| Anode | `0 ≤ Va ≤ 600 V`; `Ia ≤ min(0.2 A, 90 W / Va)` for Va > 0 | 200 mA only through 450 V; 150 mA at 600 V | This is an outer bound, not proof of every intermediate operating point; duration/SOA |
| Screen | `0 ≤ Vs ≤ 500 V`; `Is ≤ min(0.05 A, 15 W / Vs)` for Vs > 0 | 50 mA only through 300 V; 30 mA at 500 V | Cross-rail sequencing, screen dissipation and duration |
| Grid | −150…+20 V, 50 mA peak input to analysis | Endpoint magnitudes 7.5 W and 1 W if 50 mA flows | Continuous source/sink power, polarity, peak duration, repetition, stability and energy |
| Combined | `Ph + Pa + Ps + Pg + other delivered stimulus ≤ 120 W` | Every rail cap remains subordinate to combined cap | Window, reservations, tolerance, transient energy and hardware mechanism |

At exactly zero voltage, division-based current formulas are not used: current limits still apply; zero setpoint, controlled near-zero operation and discharged outputs are separate states (D021).

| Heater voltage | Current ceiling from nominal 8 A / 60 W envelope | Power at ceiling |
|---:|---:|---:|
| 5 V | 8 A | 40 W |
| 6.3 V | 8 A | 50.4 W |
| 7.5 V | 8 A | 60 W |
| 12.6 V | 4.762 A | 60 W |
| 25 V | 2.4 A | 60 W |
| 50 V | 1.2 A | 60 W |

AC numbers above are only an RMS/unity-power-factor interpretation for review. They do not specify peak switch/connector ratings. For a sine wave alone, 50 Vrms has a 70.71 V peak differential amplitude; that is not a common-mode or insulation rating.

## 3. Simultaneous scenarios

The [generated calculation snapshot](power-calculations.md) uses [the arithmetic script](../analysis/power_budget.py). All grid reservations and efficiencies are illustrative. “Fits” below means arithmetic only; it does not approve a duty cycle or hardware setting.

| Case | Heater | Anode | Screen | Grid reservation | Sum | Result |
|---|---|---|---|---:|---:|---|
| Individual maxima | 7.5 V × 8 A = 60 W | 600 V × 150 mA = 90 W | 300 V × 50 mA = 15 W | 1 W | 166 W | Exceeds 120 W by 46 W; even without grid excess is 45 W |
| Heater-heavy boundary | 7.5 V × 8 A = 60 W | 300 V × 150 mA = 45 W | 280 V × 50 mA = 14 W | 1 W | 120 W | Arithmetic boundary; no error/transient headroom |
| Anode-heavy boundary | 12 V × 2 A = 24 W | 600 V × 150 mA = 90 W | 500 V × 10 mA = 5 W | 1 W | 120 W | Arithmetic boundary; no error/transient headroom |
| Both maximum voltages | 6.3 V × 0.3 A = 1.89 W | 600 V × 150 mA = 90 W | 500 V × 30 mA = 15 W | 1 W | 107.89 W | Leaves 12.11 W before margins; voltage combination is a G2-08 Provisional target, exact continuous point unvalidated |
| Larger grid reservation | 12 V × 2 A = 24 W | 500 V × 150 mA = 75 W | 300 V × 40 mA = 12 W | 7.5 W | 118.5 W | Leaves 1.5 W; does not establish a continuous grid rating |
| First-path upper bound | 6.3 V × 0.3 A = 1.89 W | 100 V × 5 mA = 0.5 W | Disabled | 1 W reserve | 3.39 W | Planning cap for proposed prototype; actual grid consumption TBD |

With a 60 W heater and a 1 W grid reserve, no screen load, the remaining 59 W allows at most 98.33 mA at 600 V. With a 90 W anode and 15 W screen plus 1 W grid reservation, only 14 W remains for the heater. These are useful product tradeoffs for D001, not new agreed limits.

**G2-08 confirmed direction, target Provisional:** allow simultaneous 600 V anode and 500 V screen in the intended envelope without an additional mutual-exclusion rule, provided all rail, combined allocation and valve-profile limits are met. Their 90 W / 15 W caps correspond to 150 mA / 30 mA and total 105 W; the remaining 15 W must cover heater, grid and other delivered stimuli before margins. The G2-04 continuous design basis applies to eventual approved combinations, but neither this arithmetic nor confirmation validates a continuous rating. D002 remains Open for the actual supported V/I surfaces and loss/thermal evidence.

**G2-09 Agreed comparison modes:** simultaneous operation preferred, with sequential operation explicitly selectable. Reserve all active heater/electrode/stimulus paths within one Provisional 120 W main-unit ceiling. Separately attribute measurements and protection to the compared devices; timing, independent/shared supplies and detailed channel implementation remain Open. Do not automatically change to sequential mode after rejecting an infeasible simultaneous profile.

**Illustrative low-power pair, not a validated valve profile:** two anode paths at 250 V × 20 mA use 5 W each (10 W total). Two separate heaters at 6.3 V × 0.3 A add 3.78 W, with screens disabled and a hypothetical 1 W combined grid reservation. Total allocation is **14.78 W**, leaving **105.22 W** under 120 W before margins. For two sections sharing one heater, count that actual heater once instead; the reference/filament arrangement still needs review. The example does not adopt a particular valve, heater topology, current floor or grid rating, or prove that most supported profiles have this demand.

**G2-10 Agreed interpretation:** the existing 90 W anode, 15 W screen and 60 W heater capacities are shared main-unit totals, flexibly allocated subject to the combined 120 W ceiling and eventual per-path limits. Electrode/combined numbers remain Provisional; heater capability intent stays Agreed. For example, anode allocations of 60 W and 30 W exhaust the 90 W shared target and leave 30 W under the combined ceiling before heater/screen/grid demand and margins. That example is arithmetic, not a guarantee of 60 W capability on a particular channel.

**G2-11 Agreed scope:** two simultaneously active, separately measured valve sections in the current main unit, sharing the existing capacities. This supports two single-section valves or both sections of one dual-section valve; a pair of dual-section valves uses two comparison passes. Budget every energized heater, including heaters that also warm an inactive section; its electrode conditions still require a validated profile. Exact per-path voltage/current limits, physical sharing and channel implementation remain Open.

**G2-12 agreed DC bias control.** Apply the requested bias to each section and account for its own grid source demand and returned energy, including when the setpoints are linked. Equal voltage requests can result in different currents. D003 tracks the per-path and aggregate continuous and peak limits. G2-13 proposes one requested anode voltage for simultaneous comparison within the shared anode power budget. This proposal awaits confirmation.

**Agreed under G2-01 / D001:** request a complete test envelope before enabling. Reject an infeasible request with the offending limits; do not automatically move the requested operating point. The local supervisor reserves power for bounded demand in the active profile. An alternative profile requires explicit selection and revalidation.

**Protection requirements / implementation still Open:** independent local hardware protection remains mandatory. Numeric reservations, exact port/reference definitions, averaging windows, margins, trip timing and the protection mechanism require D002–D004/G3 review; the delivery boundary is Agreed under G2-02. Proposed response to demand exceeding the reservation is inhibit/log under the safety state machine; exact sequencing remains unresolved. Live power changes need a validated reservation and reviewed transition; matrix/reference changes require the reviewed de-energized condition. Protective limiting must not be reported as successful operation at unchanged requested conditions.

Hardware choices remain unselected. Possible mechanisms are independent analog power limiting, fixed locally enforced rail partitions whose sum is bounded, or an independently supervised safety controller with separate hard trips. A shared bus input limit alone is not yet proof of a 120 W *output* limit across all efficiencies, bypass supplies and stored energy. Commanded reservations alone do not detect a failed regulator.

The operational ceiling must leave a derived margin for sensor under-reading, calibration drift and trip delay: `P_command_max ≤ 120 W − ΔP_measurement − ΔP_control/transient`. These deltas are TBD; exact 120 W examples are not admissible command limits until this is resolved.

## 4. Mains and conversion losses

Two-stage illustrative model (A001): isolated front end feeds a DC bus; rail-path efficiencies are measured from that bus to the adapter boundary and include routing losses. With `Paux_bus` for control, cooling, relays and self-checks:

```text
Pbus = Ph/ηh + Pa/ηa + Ps/ηs + Pg/ηg + Paux_bus
Pmains_real = Pbus / ηfront
Conversion/routing loss = Σ[Pj × (1/ηj − 1)] + Pbus × (1/ηfront − 1)
Internal overhead = Pmains_real − Pdelivered
Smains_VA = Pmains_real / PF
Imains_rms = Pmains_real / (Vmains_rms × PF)
```

A001 assumptions for sensitivity only: ηh=85%, ηa=80%, ηs=75%, ηg=70%, ηfront=90%, Paux_bus=12 W. None is a selected supply specification. The generated table calculates each scenario's input and internal overhead. Auxiliary consumption should later be split into controller, relays, isolated converters, measurement/audio and fans, with standby/startup/run/fault/cooldown measurements. An external load fixture's independent fan/supply input is a separate line item; if fed by the main bus, include it in Paux_bus.

No mains nameplate, fuse, transformer or connector is selected from this model. G2 needs minimum/maximum input voltage, frequency, full-load efficiency maps, power factor, inrush, startup and line-dropout behavior, overload policy and margin. A constant efficiency estimate is especially weak at low load and during linear regulation.

Illustrative topology stress: a linear anode regulator dropping an untracked 600 V bus to 100 V at 200 mA would dissipate `(600−100) × 0.2 = 100 W` while delivering only 20 W. This is an algebraic warning about that hypothetical topology, not a proposed circuit. Compare tracking preregulation plus quiet postregulation, switched ranges, and other architectures only after noise, dynamics and fault requirements are resolved. No converter topology is selected.

## 5. Separate heat and stored-energy ledgers

| Location / element | Governing quantity | Thermal path / duty needed before rating |
|---|---|---|
| Front end and electrode/heater converters | Actual loss map; linear pass `ΔV × I`; switch/magnetics losses and SOA | Heatsink/chassis/air path; worst low-line, low-output/high-current and fan-failure cases |
| Wiring, matrix, socket and contacts | `I_rms² × Rpath`; AC/cathode current superposition | Local hotspots and contact degradation; heater high-current duty; Kelvin sensing where needed |
| Valve | Anode `average(vAK × iA)`, screen `average(vSK × iS)`, heater real power and grid heat as applicable | Valve limits, ventilation, guard temperature and warm-up/cooldown; no 90 W valve-dissipation assumption |
| Resistive load bank | `average(vR²)/R` or `average(iR²)R`; DC plus AC components; tolerance/tempco | **Separate rating** per resistance/channel, voltage, pulse energy and duty; internal-first placement Provisional under G2-07; heat included in main enclosure |
| Discharge network / clamp / grid sink | `Ecap = ½ C V²`; repeated dump average `E × repetition_rate`; inductive energy `½ L I²` | Pulse and continuous fault-feed capability; heatsink location; loss of fan/control power |
| Controls/audio/relays/fans | Bus power less any exported work; eventual local heat | Cooling paths and post-fault fan demand, independent of output cap |
| Separate full-load 5U4GB fixture | Roughly 130 W load dissipation estimate only | Independent fixture supply, heater, waveform, duty and heat budget; **excluded from 120 W** |
| Optional ~1,550 V PIV fixture | Voltage, leakage current and stored energy all TBD | Independent enclosure/isolation/discharge review; **excluded from main-unit envelope** |

G2-07 records the user's preference to keep the main-unit resistive bank internal. Develop this option first with the agreed fan-assisted cooling approach; final placement remains Provisional. Include bank dissipation in main-enclosure heat and its cooling/control consumption in auxiliaries. Tester-supplied resistor power remains in the combined output budget once. The earlier external recommendation was not accepted; revisit that alternative with evidence only if the internal approach cannot meet requirements.

The load bank and valve divide delivered power; their dissipation must not be added again as new main-supply demand. In a DC resistive plate circuit, the supply's delivered power divides between valve and resistor (plus wiring). An AC-coupled load can have different DC paths, so calculate the actual topology. A separately powered fixture does add separate mains demand.

Main enclosure heat is approximately internal overhead **plus the fraction of delivered output dissipated inside that enclosure**. If all loads including valve and bank are inside it, eventual heat approaches main real input power. If the valve/bank are outside, their heat is budgeted in those guarded fixtures. External fixtures can still warm the main enclosure and require proximity analysis. For the preferred internal bank, assess the bank-to-analog thermal path and airflow distribution, not just a single bulk-air temperature.

**Illustration of internal-bank heat, A001 assumptions only:** the existing anode-heavy arithmetic case delivers 120 W and calculates 178.70 W mains input, with 58.70 W conversion/auxiliary overhead. If 60 W of that already-counted output is dissipated in an internal bank and all remaining delivered power is dissipated outside, main-enclosure heat becomes approximately **118.70 W**. Input remains 178.70 W; the bank's 60 W is not added again as new supply demand. This assumed split is not a load-bank rating, valve profile or admitted test point; the case is at the Provisional ceiling before margins, and A001 efficiencies/auxiliary power are unvalidated. Other output heat inside or transferred back into the enclosure must be added according to its actual location. No fan airflow or allowable thermal resistance follows from this arithmetic alone.

**Agreed duty basis, G2-04:** continuous operation at eventual approved steady combinations without normal timeout/cooldown within defined ambient/installation conditions. Numerical continuous ratings and combinations remain unapproved; peak-only grid behavior and startup/pulse modes require separate ratings. **Agreed ambient, G2-05 / R081:** 0–40 °C, with 40 °C the hot design/test condition. Ambient reference placement and installation details remain Open; this selects no internal temperature threshold or precision temperature range. **Agreed preference, G2-06 / R082:** temperature-controlled fan-assisted cooling with heatsinks. Airflow, acoustic/vibration/electrical-noise limits, fault limits and hardware remain Open; budget fan power by operating/fault state and preserve the audio/microphonics requirements. For each dissipative element record continuous power, pulse power/energy/duration/repetition, worst ambient, thermal resistance/transient response, temperature limit, sensor location, cooldown and shutdown behavior. A time-average alone cannot establish junction, resistor pulse or contact ratings.

## 6. Review contract

G1-06 includes microphonics in scope. D022 must decide whether the controlled stimulus is manual or powered. If powered, assign its peak/continuous input, startup energy and thermal load to the appropriate main-unit auxiliary or separately powered fixture ledger. The illustrative 12 W auxiliary assumption does not establish allowance for an unspecified actuator. No wattage, fixture supply or output-ceiling change has been selected.

**Established:** arithmetic coupling, exclusion of separate fixtures, G2-01 / D001 admission/reservation policy and G2-02 delivery boundary/loss/auxiliary accounting and G2-03 no returned-energy credit with separate absorption limits, G2-04 continuous-operation design basis, G2-05 ambient 0–40 °C, and G2-06 preferred fan-assisted cooling; G2-09 simultaneous comparison preferred with selectable sequential mode and one combined budget; G2-10 shared rail capacities with flexible allocation and unchanged numerical statuses; G2-11 two simultaneously active section paths. **Design direction:** G2-07 internal-first load bank and G2-08 simultaneous 600 V anode / 500 V screen, both Provisional pending engineering evidence. **Open:** D002–D008, D009 power/float implications, D018 channel implementation/limits and D022 stimulus demand; numeric allocation remains unresolved. **Assumptions:** A001 illustrative two-stage efficiencies, unity-PF heater examples, hypothetical grid reservations. No returned-energy credit is now agreed policy; numerical absorption ratings remain Open.

**Failure modes:** omitted active heater/channel, cross-channel backfeed or coupling, silent mode fallback, excess simultaneous demand, grid sink overheating, cold-heater surge, underestimated dropout loss, failed fan, shorted load, rail backfeed, incorrect current sign, omitted auxiliary load and residual charge after mains loss.

**Verification:** independently check worksheet; later sweep line/load/waveform/ambient, measure real input/output power and per-location heat, inject overload/fan loss, and measure trip/dump energy. Compare worst-case loss maps against duty and SOA.

**Pass G2 only when:** approved tuple envelope and grid quadrants; output-boundary/window/margin; defined mains range/input bound; credible component-independent worst-case heat and duty budget; separate load-bank specification; and local enforcement concept accounting for faults. Numeric protection, component and construction details follow G3/G4 reviews.

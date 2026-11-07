# G1 requirements review decisions

Review started and completed 6 November 2026. **G1 passed under G1-09; G2 entered and not passed.**

This record captures individual user decisions. Confirmation of scope does not validate hardware, close detailed engineering limits or assign every review role. G1-01 through G1-05 confirmed interpretations without changing the baseline. G1-06 changes microphonics from optional to Agreed scope in baseline revision 0.2; [revision 0.1 is archived](../records/design-baseline-v0.1.md). Changes and their evidence are recorded in the tracker and change log.

## G1-01 — Baseline test coverage

- **Disposition:** Confirmed by the user, 6 November 2026.
- **Question reviewed:** whether the test list presented from baseline §3.2 is agreed product scope, with detailed limits still open or provisional.
- **User confirmation:** “Yes, confirm that list as agreed scope, with the detailed limits still open or provisional. Record it and walk me through the next decision.”
- **Decision:** heater continuity/current; cold and hot shorts/leakage; emission; electrode and gas/grid-current checks; transconductance, plate resistance and amplification factor; static/dynamic curves; intermittent-fault detection; matched-pair comparison and dual-section balance; diode/rectifier tests within main-unit limits; and the listed resistive-load amplifier tests are agreed scope for the completed instrument. Implementation may be staged.
- **Requirement trace:** R011–R013, R015–R021, R023–R024. Their tracker label remains **Agreed**; its evidence changes from inferred heading interpretation to explicit user confirmation. R014 directly heated valve support remains Agreed from the existing baseline; it was not a separate choice in the presented test list.
- **Details left unresolved:** ranges, bandwidths, accuracy, supported operating envelopes and acceptance criteria retain their existing Open/Provisional status. D010/D011/D018/D020 and the applicable power/safety decisions are not closed by this confirmation.
- **Scope boundaries retained:** R025 microphonics remains Open/optional; R009 full-load 5U4GB fixture stays Deferred/separate; R010 PIV fixture stays Provisional/optional/separate; R022 detailed rectifier-goal allocation stays Open.
- **Assumption trace:** A006 confirmed for the presented test list.
- **Evidence / gate impact:** user confirmation supplies product-scope evidence for part of G1; no engineering validation or downstream gate release. Other requirement interpretations and accountable owners still need review.

## G1-02 — Heater capability commitment

- **Disposition:** Confirmed by the user, 6 November 2026.
- **Question reviewed:** retain the 0–50 V, 60 W and approximately 8 A low-voltage envelope as Agreed capability requirements, or make those headline numbers Provisional pending the power review?
- **User confirmation:** “Keep the heater envelope Agreed as recommended, with waveform, noise, floating range, duty cycle and simultaneous power allocation still open. Record it and walk me through the next decision.”
- **Decision:** retain the headline heater envelope as **Agreed** capability requirements with coupled voltage/current/power limits. Approximately 8 A is a low-voltage capability; 60 W and 50 V do not imply 8 A at 50 V. For DC operation, nominal 8 A reaches 60 W at 7.5 V, and 50 V permits at most 1.2 A under the power cap. These arithmetic bounds do not establish AC waveform conventions or validated hardware performance.
- **Requirement trace:** R026 and R029 retain their Agreed labels with explicit G1-02 confirmation added. R030 remains Open and now explicitly lists duty cycle and simultaneous allocation alongside waveform/noise, regulation and floating range. R027 AC/low-noise DC modes and R028 floating/reference capability remain Agreed from the baseline; their numerical implementation limits are not closed.
- **Details left unresolved:** waveform/frequency, noise, floating range, duty cycle and simultaneous power allocation remain Open as explicitly requested. Regulation, minimum output and startup behavior also remain unresolved under the existing baseline. D001,D006,D008,D009,D021 remain Open; R035 combined 120 W ceiling remains Provisional.
- **Rationale / impact:** preserve intended heater coverage while G2 resolves sharing, duration and thermal implications. Any proposed reduction to this agreed capability requires an explicit scope change. No baseline number changed, no prototype validation claimed and no gate passed.

## G1-03 — Electrode and combined-power envelope status

- **Disposition:** Confirmed by the user, 6 November 2026.
- **Question reviewed:** retain the proposed anode, screen and grid limits and the 120 W combined-output ceiling as Provisional until G2 reconciles allocation and thermal implications?
- **User confirmation:** “Yes, keep the electrode limits and 120 W combined ceiling Provisional until G2. Record that and walk me through the next decision.”
- **Decision:** R031 anode, R032 screen, R033 grid and R035 combined-output limits remain **Provisional** architectural inputs pending explicit G2 review. R039 retains the same Provisional 120 W planning reference; the older roughly 100 W HT estimate is not reinstated. Starting G2 does not automatically promote any limit to Agreed.
- **Detailed limits retained:** anode 0–600 V, 150 mA at full voltage/up to 200 mA lower down, 90 W cap; screen 0–500 V/up to 50 mA, 15 W cap; grid −150…+20 V/up to 50 mA peak; combined heater/electrode outputs 120 W. No numerical value changed.
- **Open work:** simultaneous allocation, grid continuous/source-sink/pulse behavior, duty, thermal implications, measurement boundary and enforcement margin. R034 and D001–D004, plus related duty/thermal decisions, remain Open.
- **Rationale / boundaries:** heater/anode/screen individual caps total 165 W before grid demand, so simultaneous maxima cannot be inferred. The Agreed heater capability and local protection requirements remain intact; separate rectifier fixtures remain outside the main-unit budget.
- **Evidence / gate impact:** explicit product-owner confirmation of status, not capability validation or G2 approval. G1 remains in progress; no gate passed and no baseline text changed.

## G1-04 — Precision-target status

- **Disposition:** Confirmed by the user, 6 November 2026.
- **Question reviewed:** retain voltage accuracy ±0.1%, current accuracy ±0.5%, gain/transconductance accuracy ±1% and analyzer residual below 0.01% THD+N at 1 kHz as Provisional targets while their definitions and supporting evidence are developed?
- **User confirmation:** “Yes, keep all four precision targets Provisional while their definitions and supporting evidence are developed. Record that and walk me through the next decision.”
- **Decision:** all four numerical targets remain **Provisional** and continue to guide architecture. No target value changed and no achieved accuracy or analyzer performance is claimed.
- **Requirement trace:** R043–R046 retain Provisional status with G1-04 confirmation added. R048 and D010/D016 remain Open: measurement ranges, percentage basis, absolute error floors, bandwidth, temperature, calibration conditions, uncertainty budgets and validation evidence still need development. Analyzer signal level and measurement bandwidth also remain unresolved.
- **Retained commitments:** built-in self-check, accessible external calibration and calibration records (R040–R042), plus the traceability constraint R047, retain their existing Agreed status. This decision does not approve the proposed percent-of-reading specification form or a particular calibration policy.
- **Rationale / gate impact:** preserve precision goals while definitions and evidence establish what can be specified and demonstrated. No baseline text changed, no detailed engineering decision closed and no gate passed. G1 remains in progress.

## G1-05 — Allocation of detailed rectifier-test goals

- **Disposition:** Confirmed by the user, 6 November 2026.
- **Question reviewed:** keep R022's allocation of detailed rectifier goals Open until each test is assigned to the main unit or a separately reviewed fixture?
- **User confirmation:** “Yes, keep the detailed rectifier-test allocation Open, with the main-unit and separate-fixture scope boundaries as described. Record that and walk me through the next decision.”
- **Decision:** R022 remains **Open**. Per-section loaded drop/balance, regulation/ripple under capacitor-input or choke-input conditions, startup surge, warm-up stability and hot/cold leakage still need defined operating envelopes and allocation. This confirmation does not assign the complete set to the main unit.
- **Confirmed scope boundaries:** R021 main-unit diode/rectifier testing under load within approved limits remains **Agreed**. R009 full-load 5U4GB fixture remains **Deferred/separate**. R010 optional approximately 1,550 V PIV fixture remains **Provisional/separate**. Both separate fixtures remain outside the main-unit 120 W budget.
- **Requirement / decision trace:** R009,R010,R021,R022 retain their statuses, now with explicit G1-05 evidence. D018/D020 remain Open for detailed coverage, operating conditions, fixture design and safety review; the separation boundary is confirmed.
- **Rationale / gate impact:** preserve the agreed main-unit rectifier capability while avoiding unassigned fixture requirements entering its electrical/thermal envelope. No numeric limits, hardware implementation or validation approved. Baseline unchanged; G1 remains in progress and no gate passed.

## G1-06 — Optional microphonics/tap-test status

- **Disposition:** Inclusion confirmed by the user's latest instruction, 6 November 2026.
- **Question reviewed:** whether the optional controlled microphonics/tap test should be deferred or retained for current consideration.
- **User correction:** the initial reply was “defferred”, followed by “actually lets include it”. The later instruction supersedes the earlier reply; no Deferred status was written to the project before the correction arrived.
- **Decision:** include controlled microphonics/tap testing as **Agreed product scope**, with architecture requirements considered in the current phase. It is no longer optional/Deferred. Its inclusion does not specify a powered actuator, a manual fixture or any other stimulus mechanism.
- **Requirement / decision trace:** R025 changes **Open → Agreed**; D019 inclusion changes **Open → Agreed**. New D022 is **Open** for stimulus/fixture/interface design, repeatability, measurement conditions, acceptance criteria and implementation sequence. Other agreed audio and intermittent-fault tests remain unchanged.
- **Baseline change:** revision 0.1 archived verbatim; revision 0.2 updates §3.2 to include microphonics and adds its implementation questions to §9. No rail, power, precision or rectifier-fixture requirement changed.
- **Gate impact:** G2 must account for any eventual stimulus power/thermal demand; G3 for fixture/guard and fault behavior; G4 for interfaces; G5 for stimulus repeatability and response discrimination. Planning is included now; build/integration sequence remains Open under D022. No implementation or gate pass authorized.

## G1-07 — Functional modules versus fixed PCB boundaries

- **Disposition:** Confirmed by the user, 6 November 2026.
- **Question reviewed:** keep the proposed module-to-board partition Provisional until G3 isolation/safety and G4 interface review, without requiring one physical PCB per functional module?
- **User confirmation:** “Yes, keep the physical board partition Provisional until the safety and interface reviews, with no one-PCB-per-module requirement. Record that and walk me through the next decision.”
- **Decision:** retain R061–R067 as **Provisional physical/functional allocation** until the safety/isolation and interface reviews. There is **no one-PCB-per-module requirement**. Functions may be split or combined subject to reviewed isolation, noise, thermal, serviceability and interface constraints.
- **Requirements retained:** all agreed functional capabilities, adapter modularity, local protection independence, grounding and analog-layout constraints remain in force. Shared physical boards do not relax those requirements.
- **Trace / evidence:** R061–R067 retain Provisional status with explicit G1-07 evidence. No PCB count, board combination, connector, circuit topology or component has been chosen. The logical ICD records the confirmed interpretation.
- **Baseline / gate impact:** baseline revision 0.2 §5 already states that these are functional modules and final board count may change; no baseline text change needed. G1 remains in progress; G3/G4 must resolve the physical partition and no gate passed.

## G1-08 — Working ownership and review accountability

- **Disposition:** Confirmed by the user, 6 November 2026.
- **Question reviewed:** adopt the proposed working ownership model, or name different owners for any role?
- **User confirmation:** “confirmed”.
- **Decision:** the user is the accountable project/product owner and approver across U/E/M/F decisions. Codex prepares research, analysis, design records and available computational checks, progressing implementation only through the agreed gates.
- **Independent review:** S is a competent independent safety reviewer whose identity remains Open. The user owns arranging that appointment before G3 sign-off. Codex preparation is not recorded as independent human safety approval. The appointment is an owned unresolved action under D013, not an unassigned project responsibility.
- **Physical evidence:** bench measurements and other physical tests identify the actual tester when their test plans are released. No test operator or reviewer is claimed to have accepted an assignment now.
- **Trace / gate impact:** the role legend assigns accountability for every requirement/decision row; R071 gate ownership and D013 reviewer-appointment responsibility reference this decision. No technical requirement status or numerical limit changes. G1 remains in progress pending overall tracker/verification-plan acceptance.

## G1-09 — Requirements reconciliation and verification-plan acceptance

- **Disposition:** **Pass**, explicitly accepted by the user, 6 November 2026.
- **Question:** accept the reconciled requirements tracker and its planned verification methods as complete enough to pass G1 and enter G2?
- **User confirmation:** “Yes, G1 is accepted. Record it as passed and proceed to G2. Walk me through the power-allocation decisions one at a time, with your recommendation.”
- **Review package:** [G1 closure review](g1-closure-review.md), tracker revision 0.9, baseline revision 0.2, and confirmed decisions G1-01 through G1-08.
- **Decision / rationale:** accept the requirements reconciliation and planned verification coverage; pass G1 and enter G2. Every requirement has an ID, status, source, accountable owner or owned appointment action, and a planned verification method; conflicts and unresolved limits remain tracked for later gates. The user is the accountable approver; Codex records the disposition. Accepted revisions and hashes are recorded in [gate reviews](gate-reviews.md).
- **Status impact:** no requirement or detailed engineering decision changes status. D019 remains Agreed; the other 21 detailed decisions remain Open. Electrode limits, the 120 W ceiling and precision targets remain Provisional. Baseline revision 0.2 is unchanged; tracker revision 0.10 records this gate approval.
- **Boundaries:** this accepts coverage and verification planning, not achieved performance, safety certification, detailed numeric test criteria or any later gate. G2 must resolve power/mains/thermal questions; G3 still requires the independent reviewer and safety evidence. Parts, schematics and layout remain subject to the existing first-four-deliverables review restrictions.

Continue with [G2 decisions](g2-decisions.md), presented individually. This record does not pre-approve them.

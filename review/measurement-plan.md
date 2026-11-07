# Uncertainty budget and calibration plan

Revision 0.7 — 7 November 2026 — supporting G4/G5 draft; microphonics, fan cooling and G2-07 preferred internal-bank and G2-09 comparison-mode and G2-11 two-section effects included; **no measured accuracy claim**.

Trace: R011–R024,R040–R048; D010,D011,D016. Voltage ±0.1%, current ±0.5%, gain/gm ±1% and analyzer residual <0.01% THD+N at 1 kHz remain Provisional. Define whether each percentage is of reading, range or full scale, plus an absolute floor, before judging a circuit. Recommended specification form is `±(a × |reading| + b_range)` under stated bandwidth, temperature, warmup and calibration age; a, b and conditions require approval.

## Measurement model and evidence

Use a documented function `y = f(raw codes, reference, divider/shunt gain, offset, temperature, timing, ...)`. Correct known bias where justified, retain correction uncertainty, and list each input's units, distribution, standard uncertainty, sensitivity coefficient and correlations. Type A comes from repeated observations; Type B uses specifications/certificates/other evidence. This follows the approach described by [NIST TN1297](https://www.nist.gov/pml/nist-technical-note-1297/nist-tn-1297-2-classification-components-uncertainty) and [NIST's budget guidance](https://www.itl.nist.gov/div898/handbook/mpc/section5/mpc56.htm).

```text
uc(y)^2 = Σ[ci^2 × ui^2] + 2Σi<j[ci × cj × covariance(xi,xj)]
ci = ∂f/∂xi
U = k × uc       (coverage factor and interpretation must be stated)
Proposed acceptance: |residual error| + U ≤ approved maximum permissible error
```

Use root-sum-square only when the statistical model justifies it; hard safety limits require conservative error bounds rather than a probabilistic accuracy estimate. Certificate expanded uncertainty is converted to standard uncertainty using its stated factor. Specified bounded errors need a justified distribution; do not automatically divide every datasheet limit by √3. [NIST Type B guidance](https://physics.nist.gov/cuu/Uncertainty/typeb.html).

ADC resolution is only one contributor. Reference, offset/gain, INL, drift and dynamic behavior matter independently. [Analog Devices ADC error analysis](https://www.analog.com/en/resources/technical-articles/the-abcs-of-analog-to-digital-converters-how-adc-errors-affect-system-performance.html).

## Initial budget register

This is a populated list of required contributions with **values still Open**, not an empty promise to make a budget later. At the component/prototype gates, replace each TBD with evidence and compute separate totals for every range, common mode and test condition.

| Term | Voltage contribution | Current contribution | Evidence / evaluation | Initial value / status |
|---|---|---|---|---|
| Reference standard | Scale and calibration correction | Reference current or voltage/shunt transfer | Certificate, uncertainty factor, loading and drift; Type B | TBD / Open |
| Divider / shunt transfer | Divider ratio, voltage coefficient, loading | Shunt resistance, self-heating, burden and tempco | Ratio/resistance calibration over working voltage/current/temp | TBD / Open |
| Analog gain / offset | Front-end offset, gain, input bias | Amplifier offset/gain, thermoelectric EMFs | Zero/span and multi-point verification; temperature sweep | TBD / Open |
| ADC / reference interface | INL, residual offset/gain, reference drive settling | Same, after appropriate gain/range | Manufacturer limits plus system measurements | TBD / Open |
| Noise / repeatability | RMS noise after declared filtering | Noise/leakage floor at small currents | Repeated observations; correlated/time-dependent samples assessed | TBD / Open |
| Drift | Warmup, temperature, aging | Warmup, self-heating, aging | Repeat checks over time/environment; calibration interval evidence | TBD / Open |
| Matrix / connector / wiring | Contact resistance outside Kelvin point, leakage/loading | Parallel leakage, contact thermal EMF, current-path ambiguity | Compare bypass and full routing; contaminated/humid limits as applicable | TBD / Open |
| Common-mode rejection | Error under T/H float and converter transients | Same plus H–K/cathode return effects | Float sweep, frequency-dependent CMRR and fault recovery | TBD / Open |
| Sampling / settling | Range-switch delay, aliasing, aperture timing | V/I skew changes calculated power; event detection | Time-aligned stimulus, filter response and settling records | TBD / Open |
| Calibration residual | Interpolation/nonlinearity beyond fit | Range overlap and polarity mismatch | Independent points not used to compute corrections | TBD / Open |

Illustrative design-allocation exercise (A002, **not performance predictions**): at 100 V, if a ±0.1%-of-reading target is chosen, total permissible error would be 0.100 V before any absolute floor. Reserving half for expanded uncertainty gives a proposed `U ≤ 0.050 V`; with k=2, `uc ≤ 0.025 V`. At 100 mA, ±0.5% would be 0.500 mA; the same proposed split gives `U ≤ 0.250 mA`, `uc ≤ 0.125 mA`. Neither the 50/50 split nor k=2 is accepted yet. These totals cannot be claimed until all table terms and correlations are evaluated; allocating tiny ADC noise alone does not satisfy them.

For each range record: signal/reference nodes; maximum common mode; polarity; min useful reading; full scale; input impedance/burden; bandwidth/filter; sample rate and simultaneous/skew constraint; overrange and recovery; target a/b; u terms; U; residual bias; calibration interval; test certificate/evidence IDs. Leakage and grid-current ranges will likely require distinct treatment from 150–200 mA anode measurements; no range architecture is selected.

## Derived quantities and audio

- `gm ≈ ΔIa/ΔVg` at controlled anode/screen/heater conditions. `rp ≈ ΔVa/ΔIa` at controlled grid and other conditions. Define perturbation amplitude, linearity region, settling and drift rejection. `μ = gm × rp` may share correlated measurements; propagate covariance.
- Difference accuracy can be worse than either reading's accuracy. A 10 mA and 11 mA pair each bounded by ±0.5% has a worst-case difference error of ±0.105 mA, or 10.5% of the 1 mA change, before grid-voltage error. Correlation can reduce some gain errors but must be demonstrated. This explains why the ±1% gm goal needs its own budget.
- Gain ratios need source/output amplitude accuracy, phase/bandwidth and loading. AC RMS measurements need waveform/crest-factor and frequency specifications. Event detection needs amplitude/duration thresholds and a detection probability/false-alarm contract, not just ADC sample rate.
- 0.01% THD+N is an amplitude ratio of 0.0001 (−80 dB). Specify fundamental level, impedance, frequency, bandwidth/weighting, acquisition window, harmonic inclusion and heater mode. Allocate source distortion, analyzer residual, coupling, ADC/DAC nonlinearity, hum and noise. Coherent harmonic distortion cannot be blindly RSS-subtracted like independent noise. A loopback result includes both source and analyzer.

## Pair and section comparison

G2-09 agrees concurrent operation as the preferred mode and selectable sequential comparison; G2-11 sets concurrent capacity to two sections. A pair of dual-section valves requires two comparison passes, so include between-pass drift and inactive-section/heater conditions in its validation. Define the compared circuit conditions, per-device voltage/current results, acquisition timing/skew, bandwidth and validity rules. Operating two devices concurrently does not by itself require separate ADCs or establish time-aligned audio acquisition; the required timing must follow the measurement definition. Account for shared references, channel gain/offset mismatch, supply/load coupling and crosstalk, as well as sequential warm-up/settling and drift. Calibrate and independently verify every implemented path and relevant channel combination. Record mode and active configuration with the results, and compare both modes under controlled conditions before claiming a matching/balance uncertainty. Exact quantitative limits remain Open under D010/D016/D018.

G2-12 verification covers DC grid bias on both sections. Measure both grid-to-cathode voltages at equal and unequal setpoints. Record each voltage with its reference and path identity as the other section changes bias and load. Include channel interaction and linked-setting mismatch in the uncertainty budget.

## Calibration workflow

G1-06 adds controlled microphonics/tap measurement as Agreed scope. Its measurand and uncertainty/repeatability model remain Open under D022: stimulus method and location, fixture coupling/re-mounting, valve operating point, event timing, response bandwidth/window, background noise, metric and acceptance thresholds. Include repeated stimuli and no-stimulus controls in P-T; establish any stimulus-reference calibration needed by the chosen method. No force, acceleration, response-sensitivity or scoring limit is inferred from the existing electrical accuracy targets.

G2-06 makes fan-assisted cooling the preferred approach (R082), while noise limits and hardware remain Open. P-M/P-T must characterize electrical fan/control pickup, acoustic/mechanical coupling and temperature drift over the approved fan states/speeds, including changes of speed. Log relevant fan and temperature conditions with validation data; define the eventual metadata/interface fields under D010/D015/D022. No-stimulus microphonics controls must account for cooling background. No fan-off measurement mode or numerical noise allowance is assumed. Precision-target temperature conditions remain separate from R081's 0–40 °C power/thermal range.

G2-07 prefers an internal resistive bank. Include load heating, temperature gradients, warm-up/settling and coupled fan-state changes in the measurement/uncertainty assessment. Characterize reference, divider/shunt and low-level audio drift as bank dissipation changes within the eventual approved profiles; use consistent operating conditions for comparison. This adds future evidence needs, not an accepted drift limit or proof that internal placement meets precision targets.

1. Confirm safe connection state and calibration module identity; never infer safe access from a zero reading on the path being calibrated. Record instrument/firmware/hardware/map revisions, environment, warmup and external reference certificates/validity.
2. Run built-in self-check and save **as-found** results. Self-check detects some changes; it cannot validate the same drifting reference against itself.
3. Calibrate complete accessible signal paths, including protection, routing and selected divider/shunt ranges, at zero and enough span/intermediate points to characterize offset, gain and nonlinearity. Use both polarities where applicable; calibrate AC RMS by frequency/waveform and audio amplitude/response separately.
4. Verify with independent points/standards not used in the fit, including range overlaps and permitted common modes. Keep safety trips independently verifiable; calibration software must not move hardware protection outside approved bounds.
5. Save raw readings, coefficients, uncertainty, as-left verification, reference/module ID, date, operator, environmental conditions and pass/limited/failed validity. Detect stale, corrupted, missing or mismatched coefficients and mark results invalid rather than quietly using them.
6. Establish recalibration intervals from reference stability and measured drift; no default interval is invented. Rerun affected calibration after repairs, range/part/reference changes or failed self-checks. A plugged-in module removal aborts the sequence without committing partial coefficients.

## Pass conditions

D010/D011/D016 must define numerical range and accuracy conditions. G5 metrology passes only when every budget term has evidence, total expanded uncertainty and residual error meet the approved acceptance rule, independent points confirm the correction model, and faults/overrange do not produce apparently valid data. Precision and safety monitoring may share information, but must not create an unreviewed common failure that grants access or disables protection.

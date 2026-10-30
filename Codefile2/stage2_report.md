# Stage 2 report: reliability states and early warning

> Stage 1's primary test found no significant temporal structure beyond known conditions, so by the study design these state-space results are exploratory.

Runtime features per 1.0 s window (det_max, det_mean, ctc_mean, inter_mean, cdc_sim_mean, disagree_mean, blank_mean, entropy_mean, rms_db_mean), standardised on train. HMMs with K in [2, 3, 4, 5, 6] states fitted on train streams; **K = 2** chosen by dev log-likelihood. The HSMM has the same states with a learned dwell-time distribution up to 60 s (hazard piecewise constant on ages 1, 2–3, 4–7, … s; geometric beyond), started from the HMM. State probabilities are filtered: each uses only windows already available. Levels 1–3 are logistic regressions fitted on train and evaluated on test (speakers and noise files unseen by the KWS and by every fitted model).

## RQ2: reliability states

| K | 2 | 3 | 4 | 5 | 6 |
|---|---|---|---|---|---|
| HMM dev log-lik / window | – | – | – | – | – |

Held-out log-likelihood per window (does modelling dwell times fit runtime behaviour better?): HMM dev –, test -10.5911; HSMM dev –, test -10.5429

### HMM states on test (ordered by train FA/h at 5.0 FA/h)

| state | time % | median dwell s | FA/h train | FA/h test | det_max | entropy_mean | blank_mean | rms_db_mean | % clean | % 20 dB | % 10 dB | % 5 dB | % 0 dB |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| S1 | 53.734 | 2.0 | 0.06 | 0.144 | 0.563 | 0.417 | 0.678 | -26.582 | 23.195 | 22.688 | 20.616 | 17.989 | 15.513 |
| S2 | 46.266 | 2.0 | 9.863 | 9.651 | 0.756 | 0.27 | 0.859 | -34.205 | 20.112 | 17.104 | 19.629 | 19.605 | 23.55 |

Switch probabilities when a state is left (row = from):

| from | S1 | S2 |
|---|---|---|
| S1 | 0.0 | 1.0 |
| S2 | 1.0 | 0.0 |

### HSMM states on test (ordered by train FA/h at 5.0 FA/h)

| state | time % | median dwell s | FA/h train | FA/h test | det_max | entropy_mean | blank_mean | rms_db_mean | % clean | % 20 dB | % 10 dB | % 5 dB | % 0 dB |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| S1 | 53.705 | 2.0 | 0.074 | 0.15 | 0.563 | 0.417 | 0.678 | -26.544 | 23.12 | 22.632 | 20.624 | 18.029 | 15.594 |
| S2 | 46.295 | 2.0 | 9.836 | 9.639 | 0.755 | 0.269 | 0.859 | -34.244 | 20.201 | 17.171 | 19.62 | 19.558 | 23.45 |

Switch probabilities when a state is left (row = from):

| from | S1 | S2 |
|---|---|---|
| S1 | 0.0 | 1.0 |
| S2 | 1.0 | 0.0 |

## RQ3: early warning (pre-specified)

Target: a false accept within the next 30 s at 5.0 FA/h. Test base rate 0.0366 (3478 positive windows). Metric: average precision (chance = base rate); 95% CIs from resampling test streams.

| level | AP | 95% CI |
|---|---|---|
| L1 current window | 0.052 | 0.043–0.061 |
| L2 + moving statistics | 0.068 | 0.050–0.089 |
| L3 + HMM state | 0.068 | 0.050–0.090 |
| L3 + HSMM state | 0.068 | 0.050–0.090 |

| comparison | ΔAP | 95% CI |
|---|---|---|
| L2 + moving statistics vs L1 current window | 0.016 | 0.003–0.035 |
| L3 + HMM state vs L2 + moving statistics | 0.000 | -0.000–0.001 |
| L3 + HSMM state vs L2 + moving statistics | 0.000 | -0.000–0.001 |

**No evidence that state modelling adds early-warning information beyond Level 2.**

## Sensitivity: other horizons (test AP, same operating point)

| horizon s | base rate | L1 current window | L2 + moving statistics | L3 + HMM state | L3 + HSMM state |
|---|---|---|---|---|---|
| 1 | 0.0013 | 0.1277 | 0.1195 | 0.119 | 0.119 |
| 3 | 0.0038 | 0.0319 | 0.0235 | 0.0257 | 0.0258 |
| 5 | 0.0063 | 0.0272 | 0.0224 | 0.0236 | 0.0236 |
| 10 | 0.0126 | 0.0285 | 0.0307 | 0.0312 | 0.0312 |
| 30 | 0.0366 | 0.0521 | 0.068 | 0.0684 | 0.0684 |

## Generalisation across noise conditions (test AP at the primary horizon)

| condition | positive windows | L1 current window | L2 + moving statistics | L3 + HMM state | L3 + HSMM state |
|---|---|---|---|---|---|
| clean | 539 | 0.0644 | 0.1085 | 0.1105 | 0.1102 |
| 20 dB | 621 | 0.0615 | 0.0465 | 0.0468 | 0.0468 |
| 10 dB | 1000 | 0.0743 | 0.1085 | 0.1082 | 0.1082 |
| 5 dB | 549 | 0.0427 | 0.0566 | 0.0573 | 0.0572 |
| 0 dB | 769 | 0.0496 | 0.0551 | 0.0554 | 0.0554 |

Also unseen on test: speakers and noise files. Scope: one KWS model, 20–60 min streams, false accepts only (negative audio).

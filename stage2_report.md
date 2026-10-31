# Stage 2 report: reliability states and early warning

Runtime features per 1.0 s window (det_max, det_mean, ctc_mean, inter_mean, cdc_sim_mean, disagree_mean, blank_mean, entropy_mean, rms_db_mean), standardised on train. HMMs with K in [2, 3, 4, 5, 6] states fitted on train streams; **K = 6** chosen by dev log-likelihood. The HSMM has the same states with a learned dwell-time distribution up to 60 s (hazard piecewise constant on ages 1, 2–3, 4–7, … s; geometric beyond), started from the HMM. State probabilities are filtered: each uses only windows already available. Levels 1–3 are logistic regressions fitted on train and evaluated on test (speakers and noise files unseen by the KWS and by every fitted model).

## RQ2: reliability states

| K | 2 | 3 | 4 | 5 | 6 |
|---|---|---|---|---|---|
| HMM dev log-lik / window | -10.4212 | -9.4140 | -8.7598 | -8.1389 | -7.7797 |

Held-out log-likelihood per window (does modelling dwell times fit runtime behaviour better?): HMM dev -7.7797, test -7.8394; HSMM dev -7.7739, test -7.8330

### HMM states on test (ordered by train FA/h at 5.0 FA/h)

| state | time % | median dwell s | FA/h train | FA/h test | det_max | entropy_mean | blank_mean | rms_db_mean | % clean | % 20 dB | % 10 dB | % 5 dB | % 0 dB |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| S1 | 24.701 | 1.0 | 0.0 | 0.0 | 0.513 | 0.369 | 0.626 | -25.611 | 29.517 | 24.135 | 23.055 | 16.755 | 6.538 |
| S2 | 12.691 | 1.0 | 0.033 | 0.0 | 0.657 | 0.115 | 0.918 | -42.2 | 33.95 | 23.028 | 22.699 | 14.741 | 5.582 |
| S3 | 28.281 | 1.0 | 0.097 | 0.434 | 0.661 | 0.595 | 0.671 | -21.634 | 9.67 | 10.97 | 16.795 | 27.052 | 35.513 |
| S4 | 4.297 | 1.0 | 2.631 | 0.822 | 0.471 | 0.229 | 0.806 | -37.993 | 30.211 | 23.187 | 18.926 | 15.138 | 12.538 |
| S5 | 8.198 | 1.0 | 12.965 | 9.006 | 0.76 | 0.008 | 0.999 | -53.373 | 35.199 | 28.859 | 21.268 | 10.755 | 3.919 |
| S6 | 21.833 | 1.0 | 16.472 | 14.004 | 0.794 | 0.308 | 0.838 | -27.435 | 10.935 | 12.6 | 19.106 | 27.499 | 29.859 |

Switch probabilities when a state is left (row = from):

| from | S1 | S2 | S3 | S4 | S5 | S6 |
|---|---|---|---|---|---|---|
| S1 | 0.0 | 0.519 | 0.208 | 0.048 | 0.164 | 0.061 |
| S2 | 0.124 | 0.0 | 0.197 | 0.033 | 0.288 | 0.358 |
| S3 | 0.442 | 0.167 | 0.0 | 0.01 | 0.058 | 0.322 |
| S4 | 0.454 | 0.235 | 0.192 | 0.0 | 0.067 | 0.052 |
| S5 | 0.018 | 0.031 | 0.209 | 0.11 | 0.0 | 0.633 |
| S6 | 0.301 | 0.026 | 0.601 | 0.043 | 0.029 | 0.0 |

### HSMM states on test (ordered by train FA/h at 5.0 FA/h)

| state | time % | median dwell s | FA/h train | FA/h test | det_max | entropy_mean | blank_mean | rms_db_mean | % clean | % 20 dB | % 10 dB | % 5 dB | % 0 dB |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| S1 | 24.75 | 1.0 | 0.0 | 0.0 | 0.513 | 0.369 | 0.626 | -25.613 | 29.517 | 24.138 | 23.07 | 16.766 | 6.51 |
| S2 | 12.631 | 1.0 | 0.028 | 0.0 | 0.656 | 0.113 | 0.918 | -42.342 | 34.145 | 23.078 | 22.663 | 14.644 | 5.471 |
| S3 | 28.286 | 1.0 | 0.096 | 0.437 | 0.661 | 0.596 | 0.671 | -21.631 | 9.652 | 10.938 | 16.759 | 27.046 | 35.606 |
| S4 | 4.306 | 1.0 | 2.794 | 0.85 | 0.472 | 0.229 | 0.807 | -37.974 | 30.042 | 23.189 | 18.981 | 15.184 | 12.603 |
| S5 | 8.206 | 1.0 | 13.041 | 9.067 | 0.761 | 0.008 | 0.999 | -53.235 | 34.98 | 28.769 | 21.374 | 10.899 | 3.978 |
| S6 | 21.82 | 1.0 | 16.413 | 13.976 | 0.794 | 0.308 | 0.838 | -27.443 | 10.967 | 12.636 | 19.107 | 27.487 | 29.803 |

Switch probabilities when a state is left (row = from):

| from | S1 | S2 | S3 | S4 | S5 | S6 |
|---|---|---|---|---|---|---|
| S1 | 0.0 | 0.518 | 0.209 | 0.048 | 0.164 | 0.062 |
| S2 | 0.122 | 0.0 | 0.197 | 0.034 | 0.289 | 0.358 |
| S3 | 0.441 | 0.167 | 0.0 | 0.011 | 0.059 | 0.322 |
| S4 | 0.453 | 0.232 | 0.197 | 0.0 | 0.065 | 0.054 |
| S5 | 0.018 | 0.028 | 0.209 | 0.112 | 0.0 | 0.633 |
| S6 | 0.301 | 0.025 | 0.601 | 0.044 | 0.03 | 0.0 |

## RQ3: early warning (pre-specified)

Target: a false accept within the next 30 s at 5.0 FA/h. Test base rate 0.0307 (2879 positive windows). Metric: average precision (chance = base rate); 95% CIs from resampling test streams.

| level | AP | 95% CI |
|---|---|---|
| L1 current window | 0.045 | 0.037–0.055 |
| L2 + moving statistics | 0.056 | 0.039–0.087 |
| L3 + HMM state | 0.056 | 0.040–0.085 |
| L3 + HSMM state | 0.056 | 0.040–0.085 |

| comparison | ΔAP | 95% CI |
|---|---|---|
| L2 + moving statistics vs L1 current window | 0.011 | -0.001–0.035 |
| L3 + HMM state vs L2 + moving statistics | 0.000 | -0.002–0.001 |
| L3 + HSMM state vs L2 + moving statistics | 0.000 | -0.002–0.001 |

**No evidence that state modelling adds early-warning information beyond Level 2.**

## Sensitivity: other horizons (test AP, same operating point)

| horizon s | base rate | L1 current window | L2 + moving statistics | L3 + HMM state | L3 + HSMM state |
|---|---|---|---|---|---|
| 1 | 0.0011 | 0.1039 | 0.091 | 0.1133 | 0.1139 |
| 3 | 0.0033 | 0.023 | 0.0177 | 0.022 | 0.022 |
| 5 | 0.0054 | 0.0195 | 0.0186 | 0.0204 | 0.0204 |
| 10 | 0.0106 | 0.0234 | 0.0249 | 0.0256 | 0.0255 |
| 30 | 0.0307 | 0.045 | 0.0557 | 0.0558 | 0.0558 |

## Generalisation across noise conditions (test AP at the primary horizon)

| condition | positive windows | L1 current window | L2 + moving statistics | L3 + HMM state | L3 + HSMM state |
|---|---|---|---|---|---|
| clean | 462 | 0.0757 | 0.1314 | 0.1268 | 0.1268 |
| 20 dB | 587 | 0.0612 | 0.0487 | 0.0491 | 0.0491 |
| 10 dB | 393 | 0.0284 | 0.0479 | 0.0467 | 0.0466 |
| 5 dB | 819 | 0.0522 | 0.06 | 0.0609 | 0.0609 |
| 0 dB | 618 | 0.0418 | 0.0407 | 0.0406 | 0.0406 |

Also unseen on test: speakers and noise files. Scope: one KWS model, 20–60 min streams, false accepts only (negative audio).

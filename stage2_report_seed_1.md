# Stage 2 report: reliability states and early warning

Runtime features per 1.0 s window (det_max, det_mean, ctc_mean, inter_mean, cdc_sim_mean, disagree_mean, blank_mean, entropy_mean, rms_db_mean), standardised on train. HMMs with K in [2, 3, 4, 5, 6] states fitted on train streams; **K = 6** chosen by dev log-likelihood. The HSMM has the same states with a learned dwell-time distribution up to 60 s (hazard piecewise constant on ages 1, 2–3, 4–7, … s; geometric beyond), started from the HMM. State probabilities are filtered: each uses only windows already available. Levels 1–3 are logistic regressions fitted on train and evaluated on test (speakers and noise files unseen by the KWS and by every fitted model).

## RQ2: reliability states

| K | 2 | 3 | 4 | 5 | 6 |
|---|---|---|---|---|---|
| HMM dev log-lik / window | -10.3647 | -9.3966 | -8.7303 | -8.0876 | -7.6778 |

Held-out log-likelihood per window (does modelling dwell times fit runtime behaviour better?): HMM dev -7.6778, test -7.9619; HSMM dev -7.6717, test -7.9571

### HMM states on test (ordered by train FA/h at 5.0 FA/h)

| state | time % | median dwell s | FA/h train | FA/h test | det_max | entropy_mean | blank_mean | rms_db_mean | % clean | % 20 dB | % 10 dB | % 5 dB | % 0 dB |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| S1 | 24.677 | 1.0 | 0.0 | 0.0 | 0.513 | 0.379 | 0.627 | -25.302 | 26.607 | 23.733 | 21.536 | 17.517 | 10.607 |
| S2 | 12.366 | 1.0 | 0.053 | 0.005 | 0.657 | 0.115 | 0.92 | -41.242 | 31.672 | 22.224 | 22.029 | 16.176 | 7.898 |
| S3 | 29.196 | 1.0 | 0.351 | 0.143 | 0.66 | 0.6 | 0.673 | -21.304 | 8.413 | 9.506 | 16.19 | 25.603 | 40.288 |
| S4 | 3.854 | 1.0 | 5.727 | 3.411 | 0.494 | 0.233 | 0.813 | -37.441 | 27.02 | 19.109 | 17.576 | 18.994 | 17.301 |
| S5 | 22.178 | 1.0 | 17.999 | 16.257 | 0.793 | 0.313 | 0.837 | -26.742 | 9.621 | 11.214 | 18.429 | 25.94 | 34.796 |
| S6 | 7.727 | 1.0 | 18.355 | 15.245 | 0.764 | 0.01 | 0.999 | -50.962 | 31.922 | 24.664 | 22.543 | 14.398 | 6.473 |

Switch probabilities when a state is left (row = from):

| from | S1 | S2 | S3 | S4 | S5 | S6 |
|---|---|---|---|---|---|---|
| S1 | 0.0 | 0.523 | 0.214 | 0.037 | 0.061 | 0.165 |
| S2 | 0.118 | 0.0 | 0.201 | 0.03 | 0.363 | 0.288 |
| S3 | 0.449 | 0.168 | 0.0 | 0.007 | 0.311 | 0.065 |
| S4 | 0.479 | 0.227 | 0.194 | 0.0 | 0.053 | 0.047 |
| S5 | 0.312 | 0.026 | 0.587 | 0.038 | 0.0 | 0.036 |
| S6 | 0.02 | 0.029 | 0.196 | 0.105 | 0.649 | 0.0 |

### HSMM states on test (ordered by train FA/h at 5.0 FA/h)

| state | time % | median dwell s | FA/h train | FA/h test | det_max | entropy_mean | blank_mean | rms_db_mean | % clean | % 20 dB | % 10 dB | % 5 dB | % 0 dB |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| S1 | 24.726 | 1.0 | 0.0 | 0.0 | 0.513 | 0.379 | 0.627 | -25.3 | 26.597 | 23.712 | 21.554 | 17.545 | 10.592 |
| S2 | 12.321 | 1.0 | 0.047 | 0.005 | 0.656 | 0.113 | 0.921 | -41.407 | 31.859 | 22.305 | 22.01 | 16.071 | 7.755 |
| S3 | 29.215 | 1.0 | 0.347 | 0.139 | 0.66 | 0.6 | 0.673 | -21.306 | 8.402 | 9.496 | 16.154 | 25.591 | 40.357 |
| S4 | 3.867 | 1.0 | 5.663 | 3.411 | 0.495 | 0.233 | 0.814 | -37.432 | 26.967 | 19.083 | 17.609 | 19.004 | 17.336 |
| S5 | 22.15 | 1.0 | 17.988 | 16.246 | 0.793 | 0.313 | 0.837 | -26.74 | 9.634 | 11.238 | 18.436 | 25.934 | 34.758 |
| S6 | 7.72 | 1.0 | 18.494 | 15.358 | 0.765 | 0.01 | 0.999 | -50.818 | 31.699 | 24.572 | 22.628 | 14.533 | 6.568 |

Switch probabilities when a state is left (row = from):

| from | S1 | S2 | S3 | S4 | S5 | S6 |
|---|---|---|---|---|---|---|
| S1 | 0.0 | 0.523 | 0.215 | 0.038 | 0.061 | 0.164 |
| S2 | 0.116 | 0.0 | 0.203 | 0.031 | 0.363 | 0.288 |
| S3 | 0.448 | 0.168 | 0.0 | 0.008 | 0.31 | 0.065 |
| S4 | 0.477 | 0.227 | 0.196 | 0.0 | 0.053 | 0.046 |
| S5 | 0.312 | 0.025 | 0.587 | 0.039 | 0.0 | 0.036 |
| S6 | 0.02 | 0.028 | 0.196 | 0.106 | 0.65 | 0.0 |

## RQ3: early warning (pre-specified)

Target: a false accept within the next 30 s at 5.0 FA/h. Test base rate 0.0398 (3785 positive windows). Metric: average precision (chance = base rate); 95% CIs from resampling test streams.

| level | AP | 95% CI |
|---|---|---|
| L1 current window | 0.060 | 0.050–0.070 |
| L2 + moving statistics | 0.077 | 0.061–0.098 |
| L3 + HMM state | 0.078 | 0.061–0.099 |
| L3 + HSMM state | 0.078 | 0.061–0.099 |

| comparison | ΔAP | 95% CI |
|---|---|---|
| L2 + moving statistics vs L1 current window | 0.017 | 0.004–0.038 |
| L3 + HMM state vs L2 + moving statistics | 0.001 | 0.000–0.001 |
| L3 + HSMM state vs L2 + moving statistics | 0.001 | 0.000–0.001 |

**State modelling adds early-warning information beyond Level 2 (L3 + HMM state vs L2 + moving statistics, L3 + HSMM state vs L2 + moving statistics: CI above 0).**

## Sensitivity: other horizons (test AP, same operating point)

| horizon s | base rate | L1 current window | L2 + moving statistics | L3 + HMM state | L3 + HSMM state |
|---|---|---|---|---|---|
| 1 | 0.0014 | 0.0404 | 0.0376 | 0.0486 | 0.0487 |
| 3 | 0.0041 | 0.0225 | 0.0201 | 0.0247 | 0.0247 |
| 5 | 0.0069 | 0.0209 | 0.0217 | 0.0235 | 0.0235 |
| 10 | 0.0137 | 0.0256 | 0.0319 | 0.0329 | 0.0329 |
| 30 | 0.0398 | 0.0597 | 0.0768 | 0.0775 | 0.0775 |

## Generalisation across noise conditions (test AP at the primary horizon)

| condition | positive windows | L1 current window | L2 + moving statistics | L3 + HMM state | L3 + HSMM state |
|---|---|---|---|---|---|
| clean | 481 | 0.0508 | 0.0616 | 0.0615 | 0.0614 |
| 20 dB | 653 | 0.0867 | 0.1613 | 0.1585 | 0.1585 |
| 10 dB | 643 | 0.0544 | 0.0751 | 0.0765 | 0.0765 |
| 5 dB | 922 | 0.0723 | 0.0943 | 0.0944 | 0.0944 |
| 0 dB | 1086 | 0.0552 | 0.0574 | 0.0583 | 0.0582 |

Also unseen on test: speakers and noise files. Scope: one KWS model, 20–60 min streams, false accepts only (negative audio).

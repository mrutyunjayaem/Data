# Stage 2 report: reliability states and early warning

Runtime features per 1.0 s window (det_max, det_mean, ctc_mean, inter_mean, cdc_sim_mean, disagree_mean, blank_mean, entropy_mean, rms_db_mean), standardised on train. HMMs with K in [2, 3, 4, 5, 6] states fitted on train streams; **K = 6** chosen by dev log-likelihood. The HSMM has the same states with a learned dwell-time distribution up to 60 s (hazard piecewise constant on ages 1, 2–3, 4–7, … s; geometric beyond), started from the HMM. State probabilities are filtered: each uses only windows already available. Levels 1–3 are logistic regressions fitted on train and evaluated on test (speakers and noise files unseen by the KWS and by every fitted model).

## RQ2: reliability states

| K | 2 | 3 | 4 | 5 | 6 |
|---|---|---|---|---|---|
| HMM dev log-lik / window | -10.8319 | -9.8963 | -9.2435 | -8.3560 | -7.9185 |

Held-out log-likelihood per window (does modelling dwell times fit runtime behaviour better?): HMM dev -7.9185, test -7.8452; HSMM dev -7.9121, test -7.8394

### HMM states on test (ordered by train FA/h at 5.0 FA/h)

| state | time % | median dwell s | FA/h train | FA/h test | det_max | entropy_mean | blank_mean | rms_db_mean | % clean | % 20 dB | % 10 dB | % 5 dB | % 0 dB |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| S1 | 26.467 | 1.0 | 0.0 | 0.0 | 0.515 | 0.37 | 0.629 | -25.471 | 23.087 | 31.586 | 20.139 | 17.806 | 7.382 |
| S2 | 13.474 | 1.0 | 0.035 | 0.003 | 0.661 | 0.117 | 0.919 | -40.626 | 28.337 | 29.647 | 19.667 | 15.865 | 6.484 |
| S3 | 26.798 | 1.0 | 0.257 | 0.527 | 0.665 | 0.586 | 0.673 | -21.383 | 8.405 | 12.972 | 16.742 | 25.317 | 36.564 |
| S4 | 4.552 | 1.0 | 0.857 | 2.723 | 0.473 | 0.225 | 0.804 | -37.696 | 29.116 | 28.234 | 14.28 | 15.279 | 13.092 |
| S5 | 20.364 | 1.0 | 16.056 | 18.249 | 0.795 | 0.305 | 0.837 | -27.06 | 9.856 | 14.772 | 18.413 | 25.267 | 31.692 |
| S6 | 8.345 | 1.0 | 17.009 | 16.614 | 0.765 | 0.01 | 0.999 | -50.257 | 29.796 | 31.165 | 20.283 | 13.207 | 5.548 |

Switch probabilities when a state is left (row = from):

| from | S1 | S2 | S3 | S4 | S5 | S6 |
|---|---|---|---|---|---|---|
| S1 | 0.0 | 0.522 | 0.212 | 0.054 | 0.059 | 0.153 |
| S2 | 0.121 | 0.0 | 0.211 | 0.034 | 0.359 | 0.275 |
| S3 | 0.453 | 0.17 | 0.0 | 0.011 | 0.309 | 0.057 |
| S4 | 0.457 | 0.261 | 0.177 | 0.0 | 0.047 | 0.057 |
| S5 | 0.307 | 0.028 | 0.59 | 0.043 | 0.0 | 0.032 |
| S6 | 0.018 | 0.035 | 0.199 | 0.109 | 0.639 | 0.0 |

### HSMM states on test (ordered by train FA/h at 5.0 FA/h)

| state | time % | median dwell s | FA/h train | FA/h test | det_max | entropy_mean | blank_mean | rms_db_mean | % clean | % 20 dB | % 10 dB | % 5 dB | % 0 dB |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| S1 | 26.511 | 1.0 | 0.0 | 0.0 | 0.515 | 0.37 | 0.629 | -25.471 | 23.098 | 31.565 | 20.146 | 17.816 | 7.376 |
| S2 | 13.407 | 1.0 | 0.03 | 0.003 | 0.661 | 0.115 | 0.92 | -40.796 | 28.524 | 29.776 | 19.651 | 15.737 | 6.312 |
| S3 | 26.829 | 1.0 | 0.255 | 0.524 | 0.665 | 0.585 | 0.673 | -21.387 | 8.395 | 12.959 | 16.71 | 25.305 | 36.63 |
| S4 | 4.553 | 1.0 | 0.89 | 2.805 | 0.473 | 0.225 | 0.805 | -37.7 | 29.026 | 28.176 | 14.317 | 15.361 | 13.12 |
| S5 | 20.375 | 1.0 | 16.021 | 18.196 | 0.795 | 0.305 | 0.836 | -27.065 | 9.871 | 14.806 | 18.429 | 25.258 | 31.636 |
| S6 | 8.326 | 1.0 | 17.122 | 16.724 | 0.765 | 0.011 | 0.999 | -50.15 | 29.634 | 31.092 | 20.34 | 13.331 | 5.603 |

Switch probabilities when a state is left (row = from):

| from | S1 | S2 | S3 | S4 | S5 | S6 |
|---|---|---|---|---|---|---|
| S1 | 0.0 | 0.521 | 0.214 | 0.054 | 0.06 | 0.151 |
| S2 | 0.12 | 0.0 | 0.212 | 0.035 | 0.358 | 0.275 |
| S3 | 0.452 | 0.169 | 0.0 | 0.011 | 0.309 | 0.058 |
| S4 | 0.456 | 0.26 | 0.181 | 0.0 | 0.048 | 0.056 |
| S5 | 0.307 | 0.027 | 0.59 | 0.044 | 0.0 | 0.033 |
| S6 | 0.018 | 0.033 | 0.199 | 0.11 | 0.64 | 0.0 |

## RQ3: early warning (pre-specified)

Target: a false accept within the next 30 s at 5.0 FA/h. Test base rate 0.0431 (4101 positive windows). Metric: average precision (chance = base rate); 95% CIs from resampling test streams.

| level | AP | 95% CI |
|---|---|---|
| L1 current window | 0.059 | 0.048–0.073 |
| L2 + moving statistics | 0.078 | 0.061–0.100 |
| L3 + HMM state | 0.078 | 0.061–0.100 |
| L3 + HSMM state | 0.078 | 0.061–0.100 |

| comparison | ΔAP | 95% CI |
|---|---|---|
| L2 + moving statistics vs L1 current window | 0.019 | 0.008–0.032 |
| L3 + HMM state vs L2 + moving statistics | 0.000 | -0.001–0.001 |
| L3 + HSMM state vs L2 + moving statistics | 0.000 | -0.001–0.001 |

**No evidence that state modelling adds early-warning information beyond Level 2.**

## Sensitivity: other horizons (test AP, same operating point)

| horizon s | base rate | L1 current window | L2 + moving statistics | L3 + HMM state | L3 + HSMM state |
|---|---|---|---|---|---|
| 1 | 0.0015 | 0.119 | 0.1193 | 0.1503 | 0.1493 |
| 3 | 0.0045 | 0.0307 | 0.0238 | 0.0295 | 0.0295 |
| 5 | 0.0074 | 0.025 | 0.022 | 0.0243 | 0.0243 |
| 10 | 0.0148 | 0.0283 | 0.0314 | 0.0318 | 0.0318 |
| 30 | 0.0431 | 0.0594 | 0.0779 | 0.0783 | 0.0783 |

## Generalisation across noise conditions (test AP at the primary horizon)

| condition | positive windows | L1 current window | L2 + moving statistics | L3 + HMM state | L3 + HSMM state |
|---|---|---|---|---|---|
| clean | 462 | 0.0471 | 0.0729 | 0.0724 | 0.0725 |
| 20 dB | 752 | 0.0751 | 0.0864 | 0.0871 | 0.0872 |
| 10 dB | 957 | 0.0709 | 0.0853 | 0.0858 | 0.0858 |
| 5 dB | 996 | 0.0627 | 0.0842 | 0.0835 | 0.0835 |
| 0 dB | 934 | 0.0587 | 0.0762 | 0.0765 | 0.0766 |

Also unseen on test: speakers and noise files. Scope: one KWS model, 20–60 min streams, false accepts only (negative audio).

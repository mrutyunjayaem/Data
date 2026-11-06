# Extended Stage 2 Report

Seed: 1

## Analysis configuration

HMM candidates: [2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]
Selected HMM/HSMM K: 12
Non-temporal GMM components: 6

Existing Stage 1 temporal windows and detector outputs were reused.
No KWS retraining or detector inference was performed.

## HMM model selection

| K | Development log-likelihood/window |
|---:|---:|
| 2 | -10.364739 |
| 3 | -9.396614 |
| 4 | -8.730347 |
| 5 | -8.087566 |
| 6 | -7.677763 |
| 7 | -7.223289 |
| 8 | -6.938621 |
| 9 | -6.817168 |
| 10 | -6.627188 |
| 11 | -6.491584 |
| 12 | -6.313308 |

## HMM and HSMM held-out likelihood

| Model | Train | Dev | Test |
|---|---:|---:|---:|
| HMM | -6.303796 | -6.313308 | -6.424071 |
| HSMM | -6.300295 | -6.310020 | -6.421201 |

## Non-temporal GMM control

The GMM is fitted to standardised runtime features without transition or dwell-time modelling. Its posterior component probabilities are added to the Level 2 moving-statistics features for the early-warning comparison.

| Split | Log-likelihood/window | BIC | AIC |
|---|---:|---:|---:|
| train | -7.610442 | 3186476.09 | 3185317.69 |
| dev | -7.610224 | 1425501.23 | 1424433.78 |
| test | -7.948114 | 1525076.83 | 1524006.65 |

## Early-warning comparison

Operating point: 5.0 FA/h
Prediction horizon: 30 seconds
Test base rate: 0.03982
Positive test windows: 3785

| Model | AP | 95% CI |
|---|---:|---:|
| L1 current window | 0.05974 | 0.05003–0.07014 |
| L2 + moving statistics | 0.07678 | 0.06089–0.09800 |
| L3 + HMM state | 0.07801 | 0.06167–0.09915 |
| L3 + HSMM state | 0.07801 | 0.06167–0.09915 |
| L3 + GMM state | 0.07765 | 0.06149–0.09912 |

## Incremental AP comparisons

| Comparison | Delta AP | 95% CI |
|---|---:|---:|
| L2 + moving statistics vs L1 current window | 0.01703 | 0.00400–0.03808 |
| L3 + HMM state vs L2 + moving statistics | 0.00123 | 0.00029–0.00250 |
| L3 + HSMM state vs L2 + moving statistics | 0.00123 | 0.00029–0.00249 |
| L3 + GMM state vs L2 + moving statistics | 0.00087 | 0.00010–0.00180 |

## Sensitivity across prediction horizons

|   horizon_seconds |   base_rate |   L1 current window |   L2 + moving statistics |   L3 + HMM state |   L3 + HSMM state |   L3 + GMM state |
|------------------:|------------:|--------------------:|-------------------------:|-----------------:|------------------:|-----------------:|
|                 1 |  0.00136735 |           0.0404075 |                0.0376051 |        0.0499173 |         0.0497951 |        0.0507428 |
|                 3 |  0.0041356  |           0.0224939 |                0.0201197 |        0.0312726 |         0.0312692 |        0.0260526 |
|                 5 |  0.00686506 |           0.0209203 |                0.0217364 |        0.0260863 |         0.0260911 |        0.0246666 |
|                10 |  0.0136651  |           0.0255731 |                0.0319033 |        0.0337265 |         0.0336981 |        0.0334765 |
|                30 |  0.0398203  |           0.0597448 |                0.0767792 |        0.0780112 |         0.0780085 |        0.0776487 |

## Generalisation across noise conditions

| condition   |   positive_windows |   L1 current window |   L2 + moving statistics |   L3 + HMM state |   L3 + HSMM state |   L3 + GMM state |
|:------------|-------------------:|--------------------:|-------------------------:|-----------------:|------------------:|-----------------:|
| clean       |                481 |           0.0508297 |                0.0615673 |        0.0618275 |         0.0618387 |        0.061488  |
| 20 dB       |                653 |           0.0866567 |                0.161298  |        0.16052   |         0.160438  |        0.161891  |
| 10 dB       |                643 |           0.0544245 |                0.0751265 |        0.0770698 |         0.0770701 |        0.0767941 |
| 5 dB        |                922 |           0.072276  |                0.0942575 |        0.0950064 |         0.0950015 |        0.0951567 |
| 0 dB        |               1086 |           0.0551752 |                0.0573884 |        0.0580265 |         0.0580281 |        0.0576608 |

## Interpretation notes

- HMM K is selected using development log-likelihood.
- HSMM uses the selected HMM as its initialisation.
- GMM is non-temporal and has no transition model.
- Confidence intervals use bootstrap resampling by test stream.
- GMM component labels are arbitrary and are not reliability-state labels.
- GMM is a control, not evidence of temporal state dynamics.

All analyses reuse previously saved temporal windows.

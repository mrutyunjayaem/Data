# Extended Stage 2 Report

Seed: 0

## Analysis configuration

HMM candidates: [2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]
Selected HMM/HSMM K: 12
Non-temporal GMM components: 6

Existing Stage 1 temporal windows and detector outputs were reused.
No KWS retraining or detector inference was performed.

## HMM model selection

| K | Development log-likelihood/window |
|---:|---:|
| 2 | -10.421179 |
| 3 | -9.413965 |
| 4 | -8.759799 |
| 5 | -8.138886 |
| 6 | -7.779702 |
| 7 | -7.330827 |
| 8 | -7.042696 |
| 9 | -6.892988 |
| 10 | -6.736038 |
| 11 | -6.572949 |
| 12 | -6.425284 |

## HMM and HSMM held-out likelihood

| Model | Train | Dev | Test |
|---|---:|---:|---:|
| HMM | -6.408918 | -6.425284 | -6.464886 |
| HSMM | -6.405072 | -6.422246 | -6.462139 |

## Non-temporal GMM control

The GMM is fitted to standardised runtime features without transition or dwell-time modelling. Its posterior component probabilities are added to the Level 2 moving-statistics features for the early-warning comparison.

| Split | Log-likelihood/window | BIC | AIC |
|---|---:|---:|---:|
| train | -7.917105 | 3315595.44 | 3314437.01 |
| dev | -7.902081 | 1497696.08 | 1496627.29 |
| test | -7.963190 | 1509411.51 | 1508342.71 |

## Early-warning comparison

Operating point: 5.0 FA/h
Prediction horizon: 30 seconds
Test base rate: 0.03065
Positive test windows: 2879

| Model | AP | 95% CI |
|---|---:|---:|
| L1 current window | 0.04497 | 0.03700–0.05460 |
| L2 + moving statistics | 0.05567 | 0.03936–0.08679 |
| L3 + HMM state | 0.05660 | 0.04025–0.08489 |
| L3 + HSMM state | 0.05661 | 0.04025–0.08488 |
| L3 + GMM state | 0.05609 | 0.03963–0.08559 |

## Incremental AP comparisons

| Comparison | Delta AP | 95% CI |
|---|---:|---:|
| L2 + moving statistics vs L1 current window | 0.01071 | -0.00144–0.03528 |
| L3 + HMM state vs L2 + moving statistics | 0.00093 | -0.00245–0.00234 |
| L3 + HSMM state vs L2 + moving statistics | 0.00094 | -0.00245–0.00232 |
| L3 + GMM state vs L2 + moving statistics | 0.00041 | -0.00127–0.00092 |

## Sensitivity across prediction horizons

|   horizon_seconds |   base_rate |   L1 current window |   L2 + moving statistics |   L3 + HMM state |   L3 + HSMM state |   L3 + GMM state |
|------------------:|------------:|--------------------:|-------------------------:|-----------------:|------------------:|-----------------:|
|                 1 |  0.0010883  |           0.103858  |                0.0909552 |        0.102023  |         0.10217   |        0.103957  |
|                 3 |  0.00328773 |           0.023028  |                0.0176768 |        0.0296071 |         0.0296895 |        0.0239255 |
|                 5 |  0.00541547 |           0.0195195 |                0.0185656 |        0.0239849 |         0.0239684 |        0.0209885 |
|                10 |  0.0106018  |           0.0233714 |                0.0249381 |        0.0275721 |         0.0275696 |        0.0258579 |
|                30 |  0.0306541  |           0.0449666 |                0.0556741 |        0.0566043 |         0.0566103 |        0.0560871 |

## Generalisation across noise conditions

| condition   |   positive_windows |   L1 current window |   L2 + moving statistics |   L3 + HMM state |   L3 + HSMM state |   L3 + GMM state |
|:------------|-------------------:|--------------------:|-------------------------:|-----------------:|------------------:|-----------------:|
| clean       |                462 |           0.075727  |                0.131413  |        0.126583  |         0.126536  |        0.128882  |
| 20 dB       |                587 |           0.0612416 |                0.0487009 |        0.0495572 |         0.0495499 |        0.0492096 |
| 10 dB       |                393 |           0.0284119 |                0.0478609 |        0.0473764 |         0.0473313 |        0.0476036 |
| 5 dB        |                819 |           0.0521936 |                0.0599791 |        0.060788  |         0.0607497 |        0.0609834 |
| 0 dB        |                618 |           0.0418308 |                0.040688  |        0.041237  |         0.0412421 |        0.0405278 |

## Interpretation notes

- HMM K is selected using development log-likelihood.
- HSMM uses the selected HMM as its initialisation.
- GMM is non-temporal and has no transition model.
- Confidence intervals use bootstrap resampling by test stream.
- GMM component labels are arbitrary and are not reliability-state labels.
- GMM is a control, not evidence of temporal state dynamics.

All analyses reuse previously saved temporal windows.

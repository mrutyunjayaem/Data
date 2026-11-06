# Extended Stage 2 Report

Seed: 2

## Analysis configuration

HMM candidates: [2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]
Selected HMM/HSMM K: 12
Non-temporal GMM components: 6

Existing Stage 1 temporal windows and detector outputs were reused.
No KWS retraining or detector inference was performed.

## HMM model selection

| K | Development log-likelihood/window |
|---:|---:|
| 2 | -10.831860 |
| 3 | -9.896278 |
| 4 | -9.243507 |
| 5 | -8.355960 |
| 6 | -7.918485 |
| 7 | -7.444076 |
| 8 | -7.167144 |
| 9 | -7.052323 |
| 10 | -6.870752 |
| 11 | -6.728143 |
| 12 | -6.569583 |

## HMM and HSMM held-out likelihood

| Model | Train | Dev | Test |
|---|---:|---:|---:|
| HMM | -6.461684 | -6.569583 | -6.465933 |
| HSMM | -6.458318 | -6.566490 | -6.462956 |

## Non-temporal GMM control

The GMM is fitted to standardised runtime features without transition or dwell-time modelling. Its posterior component probabilities are added to the Level 2 moving-statistics features for the early-warning comparison.

| Split | Log-likelihood/window | BIC | AIC |
|---|---:|---:|---:|
| train | -7.742913 | 3242087.71 | 3240929.31 |
| dev | -7.856761 | 1483142.23 | 1482073.89 |
| test | -7.753312 | 1488303.92 | 1487233.70 |

## Early-warning comparison

Operating point: 5.0 FA/h
Prediction horizon: 30 seconds
Test base rate: 0.04313
Positive test windows: 4101

| Model | AP | 95% CI |
|---|---:|---:|
| L1 current window | 0.05935 | 0.04763–0.07317 |
| L2 + moving statistics | 0.07794 | 0.06055–0.10041 |
| L3 + HMM state | 0.07864 | 0.06137–0.10022 |
| L3 + HSMM state | 0.07864 | 0.06137–0.10020 |
| L3 + GMM state | 0.07832 | 0.06117–0.09955 |

## Incremental AP comparisons

| Comparison | Delta AP | 95% CI |
|---|---:|---:|
| L2 + moving statistics vs L1 current window | 0.01859 | 0.00799–0.03232 |
| L3 + HMM state vs L2 + moving statistics | 0.00070 | -0.00099–0.00166 |
| L3 + HSMM state vs L2 + moving statistics | 0.00070 | -0.00102–0.00166 |
| L3 + GMM state vs L2 + moving statistics | 0.00038 | -0.00076–0.00096 |

## Sensitivity across prediction horizons

|   horizon_seconds |   base_rate |   L1 current window |   L2 + moving statistics |   L3 + HMM state |   L3 + HSMM state |   L3 + GMM state |
|------------------:|------------:|--------------------:|-------------------------:|-----------------:|------------------:|-----------------:|
|                 1 |  0.00148159 |           0.118954  |                0.119303  |        0.146536  |         0.14659   |        0.14187   |
|                 3 |  0.00447845 |           0.0306787 |                0.0238194 |        0.0368516 |         0.0368231 |        0.0349897 |
|                 5 |  0.00743681 |           0.0250001 |                0.0220113 |        0.027391  |         0.0274029 |        0.0261393 |
|                10 |  0.0147789  |           0.0283443 |                0.0313551 |        0.0338283 |         0.033833  |        0.0328324 |
|                30 |  0.0431276  |           0.0593532 |                0.0779408 |        0.0786374 |         0.0786417 |        0.0783213 |

## Generalisation across noise conditions

| condition   |   positive_windows |   L1 current window |   L2 + moving statistics |   L3 + HMM state |   L3 + HSMM state |   L3 + GMM state |
|:------------|-------------------:|--------------------:|-------------------------:|-----------------:|------------------:|-----------------:|
| clean       |                462 |           0.0470749 |                0.0729411 |        0.0729897 |         0.0729646 |        0.0724829 |
| 20 dB       |                752 |           0.0751271 |                0.0863508 |        0.0894056 |         0.0894364 |        0.0874989 |
| 10 dB       |                957 |           0.0709341 |                0.0853391 |        0.0861289 |         0.0861284 |        0.0859205 |
| 5 dB        |                996 |           0.0626847 |                0.0842448 |        0.0820004 |         0.0819624 |        0.0822877 |
| 0 dB        |                934 |           0.058682  |                0.0761988 |        0.0760484 |         0.0760728 |        0.0769746 |

## Interpretation notes

- HMM K is selected using development log-likelihood.
- HSMM uses the selected HMM as its initialisation.
- GMM is non-temporal and has no transition model.
- Confidence intervals use bootstrap resampling by test stream.
- GMM component labels are arbitrary and are not reliability-state labels.
- GMM is a control, not evidence of temporal state dynamics.

All analyses reuse previously saved temporal windows.

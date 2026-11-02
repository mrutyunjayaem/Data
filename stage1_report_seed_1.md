# Stage 1 report: temporal dependence of false accepts

Detector score `cdc` (CDC causal: l_his=30, l_fut=0). Detections within 2.0 s form one event. Thresholds chosen on **dev** streams. **Test** streams (speakers unseen by the KWS and by anything fitted; disjoint WHAM! noise files) give the confirmatory results; **train** streams give an exploratory replication. Nulls: 200 random re-placements of each segment's false accepts within its noise block or speaker run, keeping the detector's minimum spacing between events.

## Pre-specified primary analysis

Relative risk of a false accept in the next 30 s given one in the previous 30 s, at 5.0 FA/h, on test streams, against the within-noise-block permutation null.

**RR 2.18 (95% CI 1.06–3.50), null 1.24, p = 0.010, 132 test events → significant.**

## Event counts (thresholds from dev)

| far | train | dev | test |
|---|---|---|---|
| 0.5 | 32 | 13 | 19 |
| 1.0 | 73 | 26 | 35 |
| 2.0 | 129 | 52 | 51 |
| 5.0 | 329 | 130 | 132 |

## 0.5 FA/h (threshold 0.9457)

Test: 19 events over 26.6 h. Train: 32 events over 58.1 h.  ⚠ fewer than 100 test events: low power

| Relative risk (L = H) | test | 95% CI | null block (p) | null run (p) | train (p block) |
|---|---|---|---|---|---|
| 5 s | 0.00 | 0.00–0.00 | 0.00 (1.000) | 0.00 (1.000) | 0.00 (1.000) |
| 10 s | 0.00 | 0.00–0.00 | 0.00 (1.000) | 0.00 (1.000) | 0.00 (1.000) |
| 30 s | 0.00 | 0.00–0.00 | 0.00 (1.000) | 0.00 (1.000) | 0.00 (1.000) |

| Dispersion window | test | null block (p) | train |
|---|---|---|---|
| 1 min | 0.99 | 0.99 (0.756) | 0.99 |
| 5 min | 0.94 | 0.94 (0.483) | 0.96 |
| 10 min | 0.99 | 0.92 (0.388) | 0.98 |
| 30 min | 0.85 | 0.86 (1.000) | 0.94 |

- Inter-event gap CV (1 = Poisson), test: 0.62, null 0.58 (p 0.134); train 0.91
- Episodes (gap ≤ 30 s), test: 0 with ≥2 events; 0.0% of events in them (null 0.0%, p 1.000); median duration – s
- Pre-episode change on test, z over (-10, -2) s (n=19): det_max -0.5, det_mean 0.2, ctc_mean -0.0, inter_mean 0.2, cdc_sim_mean 0.5, disagree_mean 0.5, blank_mean 0.4, entropy_mean 1.4, rms_db_mean 1.4, in_clip_frac 3.6

**Evidence summary** (descriptive, not a formal test)

- ❌ 1. Test: clustering beyond conditions (RR 30 s > within-block null, p < 0.05)
- ❌ 2. Test: post-failure risk elevated (RR 30 s 95% CI above 1)
- ❌ 3. Train replicates it (RR 30 s > 1 and within-block p < 0.05)
- ❌ 4. Test: beyond speaker effects too (RR 30 s > within-speaker-run null, p < 0.05)
- ❌ 5. Test: elevated-risk periods last (episode share > null, duration > merge window)
- ❌ 6. Test: runtime signals change before episodes (|z| > 3 for entropy, blank or energy; n >= 10)

**0/6 → INSUFFICIENT EVENTS on test (19 < 30) at this operating point**

## 1.0 FA/h (threshold 0.9309)

Test: 35 events over 26.6 h. Train: 73 events over 58.1 h.  ⚠ fewer than 100 test events: low power

| Relative risk (L = H) | test | 95% CI | null block (p) | null run (p) | train (p block) |
|---|---|---|---|---|---|
| 5 s | 0.00 | 0.00–0.00 | 0.74 (1.000) | 2.54 (1.000) | 6.37 (0.020) |
| 10 s | 0.00 | 0.00–0.00 | 0.73 (1.000) | 2.43 (1.000) | 5.26 (0.025) |
| 30 s | 2.40 | 0.00–7.51 | 0.94 (0.134) | 2.15 (0.408) | 0.70 (0.522) |

| Dispersion window | test | null block (p) | train |
|---|---|---|---|
| 1 min | 1.04 | 0.99 (0.269) | 1.01 |
| 5 min | 1.06 | 0.97 (0.065) | 0.98 |
| 10 min | 1.06 | 0.99 (0.199) | 0.99 |
| 30 min | 0.96 | 0.93 (0.612) | 0.95 |

- Inter-event gap CV (1 = Poisson), test: 0.76, null 0.72 (p 0.060); train 0.76
- Episodes (gap ≤ 30 s), test: 0 with ≥2 events; 0.0% of events in them (null 1.9%, p 1.000); median duration – s
- Pre-episode change on test, z over (-10, -2) s (n=35): det_max -0.9, det_mean -0.6, ctc_mean 0.3, inter_mean 0.3, cdc_sim_mean -0.9, disagree_mean 0.3, blank_mean 1.7, entropy_mean 0.8, rms_db_mean 0.7, in_clip_frac 3.2

**Evidence summary** (descriptive, not a formal test)

- ❌ 1. Test: clustering beyond conditions (RR 30 s > within-block null, p < 0.05)
- ❌ 2. Test: post-failure risk elevated (RR 30 s 95% CI above 1)
- ❌ 3. Train replicates it (RR 30 s > 1 and within-block p < 0.05)
- ❌ 4. Test: beyond speaker effects too (RR 30 s > within-speaker-run null, p < 0.05)
- ❌ 5. Test: elevated-risk periods last (episode share > null, duration > merge window)
- ❌ 6. Test: runtime signals change before episodes (|z| > 3 for entropy, blank or energy; n >= 10)

**0/6 → NO evidence of temporal structure beyond known conditions**

## 2.0 FA/h (threshold 0.9189)

Test: 51 events over 26.6 h. Train: 129 events over 58.1 h.  ⚠ fewer than 100 test events: low power

| Relative risk (L = H) | test | 95% CI | null block (p) | null run (p) | train (p block) |
|---|---|---|---|---|---|
| 5 s | 0.00 | 0.00–0.00 | 1.28 (1.000) | 3.70 (1.000) | 4.54 (0.045) |
| 10 s | 3.67 | 0.00–10.39 | 1.42 (0.124) | 3.31 (0.418) | 4.23 (0.025) |
| 30 s | 3.27 | 0.00–6.52 | 1.31 (0.030) | 2.97 (0.373) | 2.68 (0.035) |

| Dispersion window | test | null block (p) | train |
|---|---|---|---|
| 1 min | 1.09 | 1.01 (0.070) | 1.06 |
| 5 min | 1.16 | 1.02 (0.010) | 1.15 |
| 10 min | 1.08 | 1.05 (0.383) | 1.18 |
| 30 min | 0.84 | 0.83 (0.667) | 1.17 |

- Inter-event gap CV (1 = Poisson), test: 0.85, null 0.82 (p 0.169); train 0.92
- Episodes (gap ≤ 30 s), test: 2 with ≥2 events; 7.8% of events in them (null 4.2%, p 0.264); median duration 15.0 s
- Pre-episode change on test, z over (-10, -2) s (n=49): det_max 0.2, det_mean 0.6, ctc_mean 1.2, inter_mean 1.6, cdc_sim_mean -0.4, disagree_mean 1.5, blank_mean 2.5, entropy_mean 0.5, rms_db_mean 1.5, in_clip_frac 3.2

**Evidence summary** (descriptive, not a formal test)

- ✅ 1. Test: clustering beyond conditions (RR 30 s > within-block null, p < 0.05)
- ❌ 2. Test: post-failure risk elevated (RR 30 s 95% CI above 1)
- ✅ 3. Train replicates it (RR 30 s > 1 and within-block p < 0.05)
- ❌ 4. Test: beyond speaker effects too (RR 30 s > within-speaker-run null, p < 0.05)
- ❌ 5. Test: elevated-risk periods last (episode share > null, duration > merge window)
- ❌ 6. Test: runtime signals change before episodes (|z| > 3 for entropy, blank or energy; n >= 10)

**2/6 → PARTIAL evidence of temporal structure**

## 5.0 FA/h (threshold 0.9016)

Test: 132 events over 26.6 h. Train: 329 events over 58.1 h.

| Relative risk (L = H) | test | 95% CI | null block (p) | null run (p) | train (p block) |
|---|---|---|---|---|---|
| 5 s | 1.77 | 0.00–4.70 | 1.20 (0.244) | 1.95 (0.547) | 1.78 (0.353) |
| 10 s | 2.47 | 0.50–5.51 | 1.26 (0.065) | 2.24 (0.343) | 2.52 (0.040) |
| 30 s | 2.18 | 1.06–3.50 | 1.24 (0.010) | 1.81 (0.104) | 2.38 (0.005) |

| Dispersion window | test | null block (p) | train |
|---|---|---|---|
| 1 min | 1.13 | 1.01 (0.010) | 1.13 |
| 5 min | 1.20 | 1.08 (0.030) | 1.27 |
| 10 min | 1.19 | 1.16 (0.259) | 1.24 |
| 30 min | 1.04 | 1.02 (0.358) | 1.45 |

- Inter-event gap CV (1 = Poisson), test: 1.12, null 1.05 (p 0.010); train 1.15
- Episodes (gap ≤ 30 s), test: 9 with ≥2 events; 15.2% of events in them (null 9.2%, p 0.055); median duration 18.0 s
- Pre-episode change on test, z over (-10, -2) s (n=119): det_max 2.6, det_mean 2.8, ctc_mean 4.0, inter_mean 4.1, cdc_sim_mean 0.6, disagree_mean 2.2, blank_mean 2.4, entropy_mean 3.5, rms_db_mean 0.6, in_clip_frac 6.0

**Evidence summary** (descriptive, not a formal test)

- ✅ 1. Test: clustering beyond conditions (RR 30 s > within-block null, p < 0.05)
- ✅ 2. Test: post-failure risk elevated (RR 30 s 95% CI above 1)
- ✅ 3. Train replicates it (RR 30 s > 1 and within-block p < 0.05)
- ❌ 4. Test: beyond speaker effects too (RR 30 s > within-speaker-run null, p < 0.05)
- ❌ 5. Test: elevated-risk periods last (episode share > null, duration > merge window)
- ✅ 6. Test: runtime signals change before episodes (|z| > 3 for entropy, blank or energy; n >= 10)

**4/6 → PARTIAL evidence of temporal structure**

## Sensitivity analyses (test split, Benjamini–Hochberg across all rows)

| far | test | p | q_bh | primary |
|---|---|---|---|---|
| 0.5 | RR 5 s vs within-block null | 1.000 | 1.000 | False |
| 0.5 | RR 5 s vs within-run null | 1.000 | 1.000 | False |
| 0.5 | RR 10 s vs within-block null | 1.000 | 1.000 | False |
| 0.5 | RR 10 s vs within-run null | 1.000 | 1.000 | False |
| 0.5 | RR 30 s vs within-block null | 1.000 | 1.000 | False |
| 0.5 | RR 30 s vs within-run null | 1.000 | 1.000 | False |
| 0.5 | dispersion 1 min vs within-block null | 0.756 | 1.000 | False |
| 0.5 | dispersion 5 min vs within-block null | 0.483 | 0.799 | False |
| 0.5 | dispersion 10 min vs within-block null | 0.388 | 0.716 | False |
| 0.5 | dispersion 30 min vs within-block null | 1.000 | 1.000 | False |
| 0.5 | gap CV vs within-block null | 0.134 | 0.430 | False |
| 0.5 | episode share vs within-block null | 1.000 | 1.000 | False |
| 1.0 | RR 5 s vs within-block null | 1.000 | 1.000 | False |
| 1.0 | RR 5 s vs within-run null | 1.000 | 1.000 | False |
| 1.0 | RR 10 s vs within-block null | 1.000 | 1.000 | False |
| 1.0 | RR 10 s vs within-run null | 1.000 | 1.000 | False |
| 1.0 | RR 30 s vs within-block null | 0.134 | 0.430 | False |
| 1.0 | RR 30 s vs within-run null | 0.408 | 0.716 | False |
| 1.0 | dispersion 1 min vs within-block null | 0.269 | 0.614 | False |
| 1.0 | dispersion 5 min vs within-block null | 0.065 | 0.304 | False |
| 1.0 | dispersion 10 min vs within-block null | 0.199 | 0.562 | False |
| 1.0 | dispersion 30 min vs within-block null | 0.612 | 0.948 | False |
| 1.0 | gap CV vs within-block null | 0.060 | 0.304 | False |
| 1.0 | episode share vs within-block null | 1.000 | 1.000 | False |
| 2.0 | RR 5 s vs within-block null | 1.000 | 1.000 | False |
| 2.0 | RR 5 s vs within-run null | 1.000 | 1.000 | False |
| 2.0 | RR 10 s vs within-block null | 0.124 | 0.430 | False |
| 2.0 | RR 10 s vs within-run null | 0.418 | 0.716 | False |
| 2.0 | RR 30 s vs within-block null | 0.030 | 0.239 | False |
| 2.0 | RR 30 s vs within-run null | 0.373 | 0.716 | False |
| 2.0 | dispersion 1 min vs within-block null | 0.070 | 0.304 | False |
| 2.0 | dispersion 5 min vs within-block null | 0.010 | 0.119 | False |
| 2.0 | dispersion 10 min vs within-block null | 0.383 | 0.716 | False |
| 2.0 | dispersion 30 min vs within-block null | 0.667 | 1.000 | False |
| 2.0 | gap CV vs within-block null | 0.169 | 0.507 | False |
| 2.0 | episode share vs within-block null | 0.264 | 0.614 | False |
| 5.0 | RR 5 s vs within-block null | 0.244 | 0.614 | False |
| 5.0 | RR 5 s vs within-run null | 0.547 | 0.876 | False |
| 5.0 | RR 10 s vs within-block null | 0.065 | 0.304 | False |
| 5.0 | RR 10 s vs within-run null | 0.343 | 0.716 | False |
| 5.0 | RR 30 s vs within-block null | 0.010 | 0.119 | True |
| 5.0 | RR 30 s vs within-run null | 0.104 | 0.418 | False |
| 5.0 | dispersion 1 min vs within-block null | 0.010 | 0.119 | False |
| 5.0 | dispersion 5 min vs within-block null | 0.030 | 0.239 | False |
| 5.0 | dispersion 10 min vs within-block null | 0.259 | 0.614 | False |
| 5.0 | dispersion 30 min vs within-block null | 0.358 | 0.716 | False |
| 5.0 | gap CV vs within-block null | 0.010 | 0.119 | False |
| 5.0 | episode share vs within-block null | 0.055 | 0.304 | False |

Stage 2 (`stage2_report.md`) runs whatever the outcome: a negative result, or states that only track SNR, is also a finding.

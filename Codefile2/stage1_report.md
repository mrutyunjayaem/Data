# Stage 1 report: temporal dependence of false accepts

Detector score `cdc` (CDC causal: l_his=30, l_fut=0). Detections within 2.0 s form one event. Thresholds chosen on **dev** streams. **Test** streams (speakers unseen by the KWS and by anything fitted; disjoint WHAM! noise files) give the confirmatory results; **train** streams give an exploratory replication. Nulls: 200 random re-placements of each segment's false accepts within its noise block or speaker run, keeping the detector's minimum spacing between events.

## Pre-specified primary analysis

Relative risk of a false accept in the next 30 s given one in the previous 30 s, at 5.0 FA/h, on test streams, against the within-noise-block permutation null.

**RR 2.04 (95% CI 0.93–3.26), null 1.49, p = 0.119, 121 test events → not significant.**

## Event counts (thresholds from dev)

| far | train | dev | test |
|---|---|---|---|
| 0.5 | 21 | 14 | 9 |
| 1.0 | 44 | 27 | 16 |
| 2.0 | 91 | 53 | 46 |
| 5.0 | 262 | 131 | 121 |

## 0.5 FA/h (threshold 0.9398)

Test: 9 events over 26.6 h. Train: 21 events over 57.9 h.  ⚠ fewer than 100 test events: low power

| Relative risk (L = H) | test | 95% CI | null block (p) | null run (p) | train (p block) |
|---|---|---|---|---|---|
| 5 s | 0.00 | 0.00–0.00 | 0.00 (1.000) | 0.00 (1.000) | 0.00 (1.000) |
| 10 s | 0.00 | 0.00–0.00 | 0.00 (1.000) | 0.00 (1.000) | 0.00 (1.000) |
| 30 s | 0.00 | 0.00–0.00 | 0.00 (1.000) | 0.00 (1.000) | 0.00 (1.000) |

| Dispersion window | test | null block (p) | train |
|---|---|---|---|
| 1 min | 0.99 | 1.00 (1.000) | 0.99 |
| 5 min | 0.98 | 0.98 (0.438) | 0.97 |
| 10 min | 0.96 | 0.96 (0.453) | 1.03 |
| 30 min | 1.17 | 1.17 (0.507) | 1.20 |

- Inter-event gap CV (1 = Poisson), test: 0.18, null 0.17 (p 0.423); train 0.80
- Episodes (gap ≤ 30 s), test: 0 with ≥2 events; 0.0% of events in them (null 0.0%, p 1.000); median duration – s
- Pre-episode change on test, z over (-10, -2) s (n=8): det_max 0.0, det_mean 0.4, ctc_mean -0.1, inter_mean 0.8, cdc_sim_mean 0.9, disagree_mean 0.2, blank_mean 0.8, entropy_mean -0.7, rms_db_mean -0.2, in_clip_frac 0.4

**Evidence summary** (descriptive, not a formal test)
- ❌ 1. Test: clustering beyond conditions (RR 30 s > within-block null, p < 0.05)
- ❌ 2. Test: post-failure risk elevated (RR 30 s 95% CI above 1)
- ❌ 3. Train replicates it (RR 30 s > 1 and within-block p < 0.05)
- ❌ 4. Test: beyond speaker effects too (RR 30 s > within-speaker-run null, p < 0.05)
- ❌ 5. Test: elevated-risk periods last (episode share > null, duration > merge window)
- ❌ 6. Test: runtime signals change before episodes (|z| > 3 for entropy, blank or energy; n >= 10)

**0/6 → INSUFFICIENT EVENTS on test (9 < 30) at this operating point**

## 1.0 FA/h (threshold 0.9270)

Test: 16 events over 26.6 h. Train: 44 events over 57.9 h.  ⚠ fewer than 100 test events: low power

| Relative risk (L = H) | test | 95% CI | null block (p) | null run (p) | train (p block) |
|---|---|---|---|---|---|
| 5 s | 0.00 | 0.00–0.00 | 0.00 (1.000) | 0.00 (1.000) | 0.00 (1.000) |
| 10 s | 0.00 | 0.00–0.00 | 0.00 (1.000) | 0.00 (1.000) | 0.00 (1.000) |
| 30 s | 0.00 | 0.00–0.00 | 0.00 (1.000) | 0.00 (1.000) | 1.06 (0.542) |

| Dispersion window | test | null block (p) | train |
|---|---|---|---|
| 1 min | 0.99 | 0.99 (1.000) | 0.99 |
| 5 min | 0.96 | 0.96 (0.393) | 1.03 |
| 10 min | 0.92 | 0.91 (0.408) | 0.99 |
| 30 min | 0.89 | 0.88 (0.453) | 1.07 |

- Inter-event gap CV (1 = Poisson), test: 0.16, null 0.21 (p 0.756); train 0.91
- Episodes (gap ≤ 30 s), test: 0 with ≥2 events; 0.0% of events in them (null 0.0%, p 1.000); median duration – s
- Pre-episode change on test, z over (-10, -2) s (n=15): det_max 1.5, det_mean 1.7, ctc_mean 1.6, inter_mean 2.6, cdc_sim_mean 0.9, disagree_mean 0.4, blank_mean 1.2, entropy_mean -0.8, rms_db_mean -0.5, in_clip_frac 0.6

**Evidence summary** (descriptive, not a formal test)
- ❌ 1. Test: clustering beyond conditions (RR 30 s > within-block null, p < 0.05)
- ❌ 2. Test: post-failure risk elevated (RR 30 s 95% CI above 1)
- ❌ 3. Train replicates it (RR 30 s > 1 and within-block p < 0.05)
- ❌ 4. Test: beyond speaker effects too (RR 30 s > within-speaker-run null, p < 0.05)
- ❌ 5. Test: elevated-risk periods last (episode share > null, duration > merge window)
- ❌ 6. Test: runtime signals change before episodes (|z| > 3 for entropy, blank or energy; n >= 10)

**0/6 → INSUFFICIENT EVENTS on test (16 < 30) at this operating point**

## 2.0 FA/h (threshold 0.9144)

Test: 46 events over 26.6 h. Train: 91 events over 57.9 h.  ⚠ fewer than 100 test events: low power

| Relative risk (L = H) | test | 95% CI | null block (p) | null run (p) | train (p block) |
|---|---|---|---|---|---|
| 5 s | 7.30 | 0.00–28.73 | 1.34 (0.065) | 2.49 (0.124) | 4.02 (0.184) |
| 10 s | 1.88 | 0.00–7.64 | 1.71 (0.338) | 2.48 (0.532) | 4.05 (0.104) |
| 30 s | 3.22 | 0.00–8.94 | 1.90 (0.149) | 2.64 (0.308) | 2.52 (0.124) |

| Dispersion window | test | null block (p) | train |
|---|---|---|---|
| 1 min | 1.10 | 1.02 (0.095) | 1.06 |
| 5 min | 1.11 | 1.06 (0.174) | 1.06 |
| 10 min | 1.07 | 1.02 (0.149) | 1.10 |
| 30 min | 0.91 | 0.94 (0.746) | 1.09 |

- Inter-event gap CV (1 = Poisson), test: 0.91, null 0.88 (p 0.174); train 0.98
- Episodes (gap ≤ 30 s), test: 3 with ≥2 events; 13.0% of events in them (null 4.9%, p 0.100); median duration 26.0 s
- Pre-episode change on test, z over (-10, -2) s (n=40): det_max 1.7, det_mean 1.6, ctc_mean 3.1, inter_mean 3.0, cdc_sim_mean -0.1, disagree_mean 0.5, blank_mean 1.1, entropy_mean 0.3, rms_db_mean -0.2, in_clip_frac 0.7

**Evidence summary** (descriptive, not a formal test)
- ❌ 1. Test: clustering beyond conditions (RR 30 s > within-block null, p < 0.05)
- ❌ 2. Test: post-failure risk elevated (RR 30 s 95% CI above 1)
- ❌ 3. Train replicates it (RR 30 s > 1 and within-block p < 0.05)
- ❌ 4. Test: beyond speaker effects too (RR 30 s > within-speaker-run null, p < 0.05)
- ❌ 5. Test: elevated-risk periods last (episode share > null, duration > merge window)
- ❌ 6. Test: runtime signals change before episodes (|z| > 3 for entropy, blank or energy; n >= 10)

**0/6 → NO evidence of temporal structure beyond known conditions**

## 5.0 FA/h (threshold 0.8989)

Test: 121 events over 26.6 h. Train: 262 events over 57.9 h.

| Relative risk (L = H) | test | 95% CI | null block (p) | null run (p) | train (p block) |
|---|---|---|---|---|---|
| 5 s | 1.57 | 0.00–4.40 | 1.42 (0.408) | 2.33 (0.741) | 3.18 (0.090) |
| 10 s | 2.06 | 0.00–4.56 | 1.57 (0.209) | 2.33 (0.602) | 2.41 (0.244) |
| 30 s | 2.04 | 0.93–3.26 | 1.49 (0.119) | 1.85 (0.303) | 2.25 (0.055) |

| Dispersion window | test | null block (p) | train |
|---|---|---|---|
| 1 min | 1.09 | 1.04 (0.114) | 1.15 |
| 5 min | 1.16 | 1.09 (0.174) | 1.25 |
| 10 min | 1.08 | 1.07 (0.433) | 1.43 |
| 30 min | 1.08 | 1.09 (0.542) | 1.55 |

- Inter-event gap CV (1 = Poisson), test: 0.94, null 0.93 (p 0.284); train 1.03
- Episodes (gap ≤ 30 s), test: 6 with ≥2 events; 11.6% of events in them (null 10.3%, p 0.338); median duration 23.5 s
- Pre-episode change on test, z over (-10, -2) s (n=108): det_max 1.6, det_mean 1.1, ctc_mean 4.7, inter_mean 3.5, cdc_sim_mean -1.3, disagree_mean 0.5, blank_mean 2.9, entropy_mean 0.7, rms_db_mean -1.0, in_clip_frac 2.7

**Evidence summary** (descriptive, not a formal test)
- ❌ 1. Test: clustering beyond conditions (RR 30 s > within-block null, p < 0.05)
- ❌ 2. Test: post-failure risk elevated (RR 30 s 95% CI above 1)
- ❌ 3. Train replicates it (RR 30 s > 1 and within-block p < 0.05)
- ❌ 4. Test: beyond speaker effects too (RR 30 s > within-speaker-run null, p < 0.05)
- ❌ 5. Test: elevated-risk periods last (episode share > null, duration > merge window)
- ❌ 6. Test: runtime signals change before episodes (|z| > 3 for entropy, blank or energy; n >= 10)

**0/6 → NO evidence of temporal structure beyond known conditions**

## Sensitivity analyses (test split, Benjamini–Hochberg across all rows)

| far | test | p | q_bh | primary |
|---|---|---|---|---|
| 0.5 | RR 5 s vs within-block null | 1.000 | 1.000 | False |
| 0.5 | RR 5 s vs within-run null | 1.000 | 1.000 | False |
| 0.5 | RR 10 s vs within-block null | 1.000 | 1.000 | False |
| 0.5 | RR 10 s vs within-run null | 1.000 | 1.000 | False |
| 0.5 | RR 30 s vs within-block null | 1.000 | 1.000 | False |
| 0.5 | RR 30 s vs within-run null | 1.000 | 1.000 | False |
| 0.5 | dispersion 1 min vs within-block null | 1.000 | 1.000 | False |
| 0.5 | dispersion 5 min vs within-block null | 0.438 | 0.869 | False |
| 0.5 | dispersion 10 min vs within-block null | 0.453 | 0.869 | False |
| 0.5 | dispersion 30 min vs within-block null | 0.507 | 0.930 | False |
| 0.5 | gap CV vs within-block null | 0.423 | 0.869 | False |
| 0.5 | episode share vs within-block null | 1.000 | 1.000 | False |
| 1.0 | RR 5 s vs within-block null | 1.000 | 1.000 | False |
| 1.0 | RR 5 s vs within-run null | 1.000 | 1.000 | False |
| 1.0 | RR 10 s vs within-block null | 1.000 | 1.000 | False |
| 1.0 | RR 10 s vs within-run null | 1.000 | 1.000 | False |
| 1.0 | RR 30 s vs within-block null | 1.000 | 1.000 | False |
| 1.0 | RR 30 s vs within-run null | 1.000 | 1.000 | False |
| 1.0 | dispersion 1 min vs within-block null | 1.000 | 1.000 | False |
| 1.0 | dispersion 5 min vs within-block null | 0.393 | 0.869 | False |
| 1.0 | dispersion 10 min vs within-block null | 0.408 | 0.869 | False |
| 1.0 | dispersion 30 min vs within-block null | 0.453 | 0.869 | False |
| 1.0 | gap CV vs within-block null | 0.756 | 1.000 | False |
| 1.0 | episode share vs within-block null | 1.000 | 1.000 | False |
| 2.0 | RR 5 s vs within-block null | 0.065 | 0.760 | False |
| 2.0 | RR 5 s vs within-run null | 0.124 | 0.760 | False |
| 2.0 | RR 10 s vs within-block null | 0.338 | 0.869 | False |
| 2.0 | RR 10 s vs within-run null | 0.532 | 0.930 | False |
| 2.0 | RR 30 s vs within-block null | 0.149 | 0.760 | False |
| 2.0 | RR 30 s vs within-run null | 0.308 | 0.869 | False |
| 2.0 | dispersion 1 min vs within-block null | 0.095 | 0.760 | False |
| 2.0 | dispersion 5 min vs within-block null | 0.174 | 0.760 | False |
| 2.0 | dispersion 10 min vs within-block null | 0.149 | 0.760 | False |
| 2.0 | dispersion 30 min vs within-block null | 0.746 | 1.000 | False |
| 2.0 | gap CV vs within-block null | 0.174 | 0.760 | False |
| 2.0 | episode share vs within-block null | 0.100 | 0.760 | False |
| 5.0 | RR 5 s vs within-block null | 0.408 | 0.869 | False |
| 5.0 | RR 5 s vs within-run null | 0.741 | 1.000 | False |
| 5.0 | RR 10 s vs within-block null | 0.209 | 0.836 | False |
| 5.0 | RR 10 s vs within-run null | 0.602 | 0.996 | False |
| 5.0 | RR 30 s vs within-block null | 0.119 | 0.760 | True |
| 5.0 | RR 30 s vs within-run null | 0.303 | 0.869 | False |
| 5.0 | dispersion 1 min vs within-block null | 0.114 | 0.760 | False |
| 5.0 | dispersion 5 min vs within-block null | 0.174 | 0.760 | False |
| 5.0 | dispersion 10 min vs within-block null | 0.433 | 0.869 | False |
| 5.0 | dispersion 30 min vs within-block null | 0.542 | 0.930 | False |
| 5.0 | gap CV vs within-block null | 0.284 | 0.869 | False |
| 5.0 | episode share vs within-block null | 0.338 | 0.869 | False |

Stage 2 (`stage2_report.md`) runs whatever the outcome: a negative result, or states that only track SNR, is also a finding.

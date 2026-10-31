# Stage 1 report: temporal dependence of false accepts

Detector score `cdc` (CDC causal: l_his=30, l_fut=0). Detections within 2.0 s form one event. Thresholds chosen on **dev** streams. **Test** streams (speakers unseen by the KWS and by anything fitted; disjoint WHAM! noise files) give the confirmatory results; **train** streams give an exploratory replication. Nulls: 200 random re-placements of each segment's false accepts within its noise block or speaker run, keeping the detector's minimum spacing between events.

## Pre-specified primary analysis

Relative risk of a false accept in the next 30 s given one in the previous 30 s, at 5.0 FA/h, on test streams, against the within-noise-block permutation null.

**RR 2.11 (95% CI 1.01–3.21), null 1.13, p = 0.010, 104 test events → significant.**

## Event counts (thresholds from dev)

| far | train | dev | test |
|---|---|---|---|
| 0.5 | 25 | 14 | 11 |
| 1.0 | 53 | 27 | 16 |
| 2.0 | 116 | 53 | 43 |
| 5.0 | 271 | 132 | 104 |

## 0.5 FA/h (threshold 0.9555)

Test: 11 events over 26.3 h. Train: 25 events over 58.1 h.  ⚠ fewer than 100 test events: low power

| Relative risk (L = H) | test | 95% CI | null block (p) | null run (p) | train (p block) |
|---|---|---|---|---|---|
| 5 s | 0.00 | 0.00–0.00 | 0.00 (1.000) | 0.00 (1.000) | 0.00 (1.000) |
| 10 s | 0.00 | 0.00–0.00 | 0.00 (1.000) | 0.00 (1.000) | 0.00 (1.000) |
| 30 s | 0.00 | 0.00–0.00 | 0.00 (1.000) | 0.00 (1.000) | 0.00 (1.000) |

| Dispersion window | test | null block (p) | train |
|---|---|---|---|
| 1 min | 0.99 | 0.99 (1.000) | 0.99 |
| 5 min | 0.97 | 0.97 (1.000) | 0.97 |
| 10 min | 0.93 | 0.93 (1.000) | 0.93 |
| 30 min | 0.80 | 0.80 (1.000) | 1.15 |

- Inter-event gap CV (1 = Poisson), test: –, null – (p –); train 0.55
- Episodes (gap ≤ 30 s), test: 0 with ≥2 events; 0.0% of events in them (null 0.0%, p 1.000); median duration – s
- Pre-episode change on test, z over (-10, -2) s (n=10): det_max 0.4, det_mean 0.5, ctc_mean 1.3, inter_mean 1.0, cdc_sim_mean -1.0, disagree_mean 1.0, blank_mean 0.1, entropy_mean 3.5, rms_db_mean 1.1, in_clip_frac 2.7

**Evidence summary** (descriptive, not a formal test)

- ❌ 1. Test: clustering beyond conditions (RR 30 s > within-block null, p < 0.05)
- ❌ 2. Test: post-failure risk elevated (RR 30 s 95% CI above 1)
- ❌ 3. Train replicates it (RR 30 s > 1 and within-block p < 0.05)
- ❌ 4. Test: beyond speaker effects too (RR 30 s > within-speaker-run null, p < 0.05)
- ❌ 5. Test: elevated-risk periods last (episode share > null, duration > merge window)
- ✅ 6. Test: runtime signals change before episodes (|z| > 3 for entropy, blank or energy; n >= 10)

**1/6 → INSUFFICIENT EVENTS on test (11 < 30) at this operating point**

## 1.0 FA/h (threshold 0.9383)

Test: 16 events over 26.3 h. Train: 53 events over 58.1 h.  ⚠ fewer than 100 test events: low power

| Relative risk (L = H) | test | 95% CI | null block (p) | null run (p) | train (p block) |
|---|---|---|---|---|---|
| 5 s | 0.00 | 0.00–0.00 | 0.00 (1.000) | 0.00 (1.000) | 8.92 (0.050) |
| 10 s | 0.00 | 0.00–0.00 | 0.00 (1.000) | 0.00 (1.000) | 5.27 (0.055) |
| 30 s | 0.00 | 0.00–0.00 | 0.00 (1.000) | 0.00 (1.000) | 1.74 (0.239) |

| Dispersion window | test | null block (p) | train |
|---|---|---|---|
| 1 min | 0.99 | 0.99 (1.000) | 1.02 |
| 5 min | 0.95 | 0.95 (1.000) | 1.00 |
| 10 min | 0.90 | 0.90 (0.090) | 0.97 |
| 30 min | 0.69 | 0.69 (1.000) | 1.24 |

- Inter-event gap CV (1 = Poisson), test: –, null – (p –); train 0.82
- Episodes (gap ≤ 30 s), test: 0 with ≥2 events; 0.0% of events in them (null 0.0%, p 1.000); median duration – s
- Pre-episode change on test, z over (-10, -2) s (n=15): det_max 0.9, det_mean 0.9, ctc_mean 1.9, inter_mean 1.7, cdc_sim_mean -0.6, disagree_mean 1.3, blank_mean 0.8, entropy_mean 2.9, rms_db_mean -0.3, in_clip_frac 3.2

**Evidence summary** (descriptive, not a formal test)

- ❌ 1. Test: clustering beyond conditions (RR 30 s > within-block null, p < 0.05)
- ❌ 2. Test: post-failure risk elevated (RR 30 s 95% CI above 1)
- ❌ 3. Train replicates it (RR 30 s > 1 and within-block p < 0.05)
- ❌ 4. Test: beyond speaker effects too (RR 30 s > within-speaker-run null, p < 0.05)
- ❌ 5. Test: elevated-risk periods last (episode share > null, duration > merge window)
- ❌ 6. Test: runtime signals change before episodes (|z| > 3 for entropy, blank or energy; n >= 10)

**0/6 → INSUFFICIENT EVENTS on test (16 < 30) at this operating point**

## 2.0 FA/h (threshold 0.9205)

Test: 43 events over 26.3 h. Train: 116 events over 58.1 h.  ⚠ fewer than 100 test events: low power

| Relative risk (L = H) | test | 95% CI | null block (p) | null run (p) | train (p block) |
|---|---|---|---|---|---|
| 5 s | 16.58 | 0.00–35.44 | 1.28 (0.010) | 3.28 (0.010) | 4.34 (0.139) |
| 10 s | 6.55 | 0.00–14.49 | 1.28 (0.020) | 3.65 (0.144) | 3.64 (0.075) |
| 30 s | 2.17 | 0.00–6.23 | 1.33 (0.214) | 2.48 (0.617) | 1.71 (0.433) |

| Dispersion window | test | null block (p) | train |
|---|---|---|---|
| 1 min | 1.11 | 1.00 (0.010) | 1.06 |
| 5 min | 1.05 | 1.01 (0.353) | 1.14 |
| 10 min | 0.95 | 1.02 (0.905) | 1.08 |
| 30 min | 1.09 | 1.15 (1.000) | 1.26 |

- Inter-event gap CV (1 = Poisson), test: 0.74, null 0.74 (p 0.532); train 0.97
- Episodes (gap ≤ 30 s), test: 3 with ≥2 events; 14.0% of events in them (null 3.3%, p 0.020); median duration 6.0 s
- Pre-episode change on test, z over (-10, -2) s (n=39): det_max 1.7, det_mean 1.4, ctc_mean 3.3, inter_mean 3.3, cdc_sim_mean -0.8, disagree_mean 1.9, blank_mean 1.9, entropy_mean 3.7, rms_db_mean -0.4, in_clip_frac 3.6

**Evidence summary** (descriptive, not a formal test)

- ❌ 1. Test: clustering beyond conditions (RR 30 s > within-block null, p < 0.05)
- ❌ 2. Test: post-failure risk elevated (RR 30 s 95% CI above 1)
- ❌ 3. Train replicates it (RR 30 s > 1 and within-block p < 0.05)
- ❌ 4. Test: beyond speaker effects too (RR 30 s > within-speaker-run null, p < 0.05)
- ✅ 5. Test: elevated-risk periods last (episode share > null, duration > merge window)
- ✅ 6. Test: runtime signals change before episodes (|z| > 3 for entropy, blank or energy; n >= 10)

**2/6 → NO evidence of temporal structure beyond known conditions**

## 5.0 FA/h (threshold 0.9062)

Test: 104 events over 26.3 h. Train: 271 events over 58.1 h.

| Relative risk (L = H) | test | 95% CI | null block (p) | null run (p) | train (p block) |
|---|---|---|---|---|---|
| 5 s | 7.21 | 0.00–16.24 | 1.12 (0.005) | 4.16 (0.050) | 4.48 (0.005) |
| 10 s | 2.38 | 0.18–5.19 | 1.19 (0.085) | 3.36 (0.836) | 4.02 (0.005) |
| 30 s | 2.11 | 1.01–3.21 | 1.13 (0.010) | 2.25 (0.632) | 2.02 (0.050) |

| Dispersion window | test | null block (p) | train |
|---|---|---|---|
| 1 min | 1.17 | 1.01 (0.005) | 1.14 |
| 5 min | 1.16 | 1.04 (0.025) | 1.27 |
| 10 min | 1.12 | 1.02 (0.025) | 1.28 |
| 30 min | 0.88 | 0.83 (0.144) | 1.30 |

- Inter-event gap CV (1 = Poisson), test: 0.93, null 0.93 (p 0.463); train 1.11
- Episodes (gap ≤ 30 s), test: 9 with ≥2 events; 19.2% of events in them (null 7.0%, p 0.005); median duration 20.0 s
- Pre-episode change on test, z over (-10, -2) s (n=90): det_max 1.8, det_mean 1.3, ctc_mean 3.1, inter_mean 2.8, cdc_sim_mean -0.8, disagree_mean 1.6, blank_mean 1.8, entropy_mean 4.0, rms_db_mean 0.7, in_clip_frac 4.8

**Evidence summary** (descriptive, not a formal test)

- ✅ 1. Test: clustering beyond conditions (RR 30 s > within-block null, p < 0.05)
- ✅ 2. Test: post-failure risk elevated (RR 30 s 95% CI above 1)
- ✅ 3. Train replicates it (RR 30 s > 1 and within-block p < 0.05)
- ❌ 4. Test: beyond speaker effects too (RR 30 s > within-speaker-run null, p < 0.05)
- ✅ 5. Test: elevated-risk periods last (episode share > null, duration > merge window)
- ✅ 6. Test: runtime signals change before episodes (|z| > 3 for entropy, blank or energy; n >= 10)

**5/6 → STRONG evidence of temporal structure beyond known conditions**

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
| 0.5 | dispersion 5 min vs within-block null | 1.000 | 1.000 | False |
| 0.5 | dispersion 10 min vs within-block null | 1.000 | 1.000 | False |
| 0.5 | dispersion 30 min vs within-block null | 1.000 | 1.000 | False |
| 0.5 | gap CV vs within-block null | – | – | False |
| 0.5 | episode share vs within-block null | 1.000 | 1.000 | False |
| 1.0 | RR 5 s vs within-block null | 1.000 | 1.000 | False |
| 1.0 | RR 5 s vs within-run null | 1.000 | 1.000 | False |
| 1.0 | RR 10 s vs within-block null | 1.000 | 1.000 | False |
| 1.0 | RR 10 s vs within-run null | 1.000 | 1.000 | False |
| 1.0 | RR 30 s vs within-block null | 1.000 | 1.000 | False |
| 1.0 | RR 30 s vs within-run null | 1.000 | 1.000 | False |
| 1.0 | dispersion 1 min vs within-block null | 1.000 | 1.000 | False |
| 1.0 | dispersion 5 min vs within-block null | 1.000 | 1.000 | False |
| 1.0 | dispersion 10 min vs within-block null | 0.090 | 0.294 | False |
| 1.0 | dispersion 30 min vs within-block null | 1.000 | 1.000 | False |
| 1.0 | gap CV vs within-block null | – | – | False |
| 1.0 | episode share vs within-block null | 1.000 | 1.000 | False |
| 2.0 | RR 5 s vs within-block null | 0.010 | 0.065 | False |
| 2.0 | RR 5 s vs within-run null | 0.010 | 0.065 | False |
| 2.0 | RR 10 s vs within-block null | 0.020 | 0.102 | False |
| 2.0 | RR 10 s vs within-run null | 0.144 | 0.415 | False |
| 2.0 | RR 30 s vs within-block null | 0.214 | 0.579 | False |
| 2.0 | RR 30 s vs within-run null | 0.617 | 1.000 | False |
| 2.0 | dispersion 1 min vs within-block null | 0.010 | 0.065 | False |
| 2.0 | dispersion 5 min vs within-block null | 0.353 | 0.903 | False |
| 2.0 | dispersion 10 min vs within-block null | 0.905 | 1.000 | False |
| 2.0 | dispersion 30 min vs within-block null | 1.000 | 1.000 | False |
| 2.0 | gap CV vs within-block null | 0.532 | 1.000 | False |
| 2.0 | episode share vs within-block null | 0.020 | 0.102 | False |
| 5.0 | RR 5 s vs within-block null | 0.005 | 0.065 | False |
| 5.0 | RR 5 s vs within-run null | 0.050 | 0.191 | False |
| 5.0 | RR 10 s vs within-block null | 0.085 | 0.294 | False |
| 5.0 | RR 10 s vs within-run null | 0.836 | 1.000 | False |
| 5.0 | RR 30 s vs within-block null | 0.010 | 0.065 | True |
| 5.0 | RR 30 s vs within-run null | 0.632 | 1.000 | False |
| 5.0 | dispersion 1 min vs within-block null | 0.005 | 0.065 | False |
| 5.0 | dispersion 5 min vs within-block null | 0.025 | 0.104 | False |
| 5.0 | dispersion 10 min vs within-block null | 0.025 | 0.104 | False |
| 5.0 | dispersion 30 min vs within-block null | 0.144 | 0.415 | False |
| 5.0 | gap CV vs within-block null | 0.463 | 1.000 | False |
| 5.0 | episode share vs within-block null | 0.005 | 0.065 | False |

Stage 2 (`stage2_report.md`) runs whatever the outcome: a negative result, or states that only track SNR, is also a finding.

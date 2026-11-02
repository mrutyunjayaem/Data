# Stage 1 report: temporal dependence of false accepts

Detector score `cdc` (CDC causal: l_his=30, l_fut=0). Detections within 2.0 s form one event. Thresholds chosen on **dev** streams. **Test** streams (speakers unseen by the KWS and by anything fitted; disjoint WHAM! noise files) give the confirmatory results; **train** streams give an exploratory replication. Nulls: 200 random re-placements of each segment's false accepts within its noise block or speaker run, keeping the detector's minimum spacing between events.

## Pre-specified primary analysis

Relative risk of a false accept in the next 30 s given one in the previous 30 s, at 5.0 FA/h, on test streams, against the within-noise-block permutation null.

**RR 1.83 (95% CI 1.03–2.67), null 1.28, p = 0.045, 143 test events → significant.**

## Event counts (thresholds from dev)

| far | train | dev | test |
|---|---|---|---|
| 0.5 | 18 | 14 | 7 |
| 1.0 | 69 | 27 | 30 |
| 2.0 | 111 | 53 | 51 |
| 5.0 | 276 | 131 | 143 |

## 0.5 FA/h (threshold 0.9514)

Test: 7 events over 26.6 h. Train: 18 events over 58.1 h.  ⚠ fewer than 100 test events: low power

| Relative risk (L = H) | test | 95% CI | null block (p) | null run (p) | train (p block) |
|---|---|---|---|---|---|
| 5 s | 0.00 | 0.00–0.00 | 0.00 (1.000) | 0.00 (1.000) | 0.00 (1.000) |
| 10 s | 0.00 | 0.00–0.00 | 0.00 (1.000) | 0.00 (1.000) | 0.00 (1.000) |
| 30 s | 0.00 | 0.00–0.00 | 0.00 (1.000) | 0.00 (1.000) | 0.00 (1.000) |

| Dispersion window | test | null block (p) | train |
|---|---|---|---|
| 1 min | 1.00 | 1.00 (1.000) | 1.00 |
| 5 min | 0.98 | 0.98 (1.000) | 0.97 |
| 10 min | 0.96 | 0.96 (0.313) | 0.95 |
| 30 min | 0.88 | 0.88 (1.000) | 1.41 |

- Inter-event gap CV (1 = Poisson), test: –, null – (p –); train 0.46
- Episodes (gap ≤ 30 s), test: 0 with ≥2 events; 0.0% of events in them (null 0.0%, p 1.000); median duration – s
- Pre-episode change on test, z over (-10, -2) s (n=7): det_max -0.3, det_mean -0.2, ctc_mean 0.1, inter_mean 0.1, cdc_sim_mean -0.4, disagree_mean 1.3, blank_mean 0.5, entropy_mean -1.1, rms_db_mean 0.6, in_clip_frac 1.9

**Evidence summary** (descriptive, not a formal test)

- ❌ 1. Test: clustering beyond conditions (RR 30 s > within-block null, p < 0.05)
- ❌ 2. Test: post-failure risk elevated (RR 30 s 95% CI above 1)
- ❌ 3. Train replicates it (RR 30 s > 1 and within-block p < 0.05)
- ❌ 4. Test: beyond speaker effects too (RR 30 s > within-speaker-run null, p < 0.05)
- ❌ 5. Test: elevated-risk periods last (episode share > null, duration > merge window)
- ❌ 6. Test: runtime signals change before episodes (|z| > 3 for entropy, blank or energy; n >= 10)

**0/6 → INSUFFICIENT EVENTS on test (7 < 30) at this operating point**

## 1.0 FA/h (threshold 0.9289)

Test: 30 events over 26.6 h. Train: 69 events over 58.1 h.  ⚠ fewer than 100 test events: low power

| Relative risk (L = H) | test | 95% CI | null block (p) | null run (p) | train (p block) |
|---|---|---|---|---|---|
| 5 s | 0.00 | 0.00–0.00 | 0.47 (1.000) | 2.28 (1.000) | 0.00 (1.000) |
| 10 s | 0.00 | 0.00–0.00 | 0.67 (1.000) | 1.95 (1.000) | 0.00 (1.000) |
| 30 s | 2.59 | 0.00–7.84 | 0.66 (0.090) | 1.40 (0.229) | 1.69 (0.080) |

| Dispersion window | test | null block (p) | train |
|---|---|---|---|
| 1 min | 0.98 | 0.99 (1.000) | 0.98 |
| 5 min | 0.97 | 0.97 (0.781) | 0.99 |
| 10 min | 0.94 | 0.91 (0.532) | 0.99 |
| 30 min | 0.83 | 0.83 (1.000) | 0.93 |

- Inter-event gap CV (1 = Poisson), test: 0.66, null 0.64 (p 0.289); train 0.74
- Episodes (gap ≤ 30 s), test: 0 with ≥2 events; 0.0% of events in them (null 1.0%, p 1.000); median duration – s
- Pre-episode change on test, z over (-10, -2) s (n=29): det_max -1.1, det_mean -1.3, ctc_mean -0.9, inter_mean -0.7, cdc_sim_mean -1.2, disagree_mean 1.4, blank_mean 0.8, entropy_mean -0.9, rms_db_mean -0.2, in_clip_frac 1.3

**Evidence summary** (descriptive, not a formal test)

- ❌ 1. Test: clustering beyond conditions (RR 30 s > within-block null, p < 0.05)
- ❌ 2. Test: post-failure risk elevated (RR 30 s 95% CI above 1)
- ❌ 3. Train replicates it (RR 30 s > 1 and within-block p < 0.05)
- ❌ 4. Test: beyond speaker effects too (RR 30 s > within-speaker-run null, p < 0.05)
- ❌ 5. Test: elevated-risk periods last (episode share > null, duration > merge window)
- ❌ 6. Test: runtime signals change before episodes (|z| > 3 for entropy, blank or energy; n >= 10)

**0/6 → NO evidence of temporal structure beyond known conditions**

## 2.0 FA/h (threshold 0.9199)

Test: 51 events over 26.6 h. Train: 111 events over 58.1 h.  ⚠ fewer than 100 test events: low power

| Relative risk (L = H) | test | 95% CI | null block (p) | null run (p) | train (p block) |
|---|---|---|---|---|---|
| 5 s | 0.00 | 0.00–0.00 | 1.01 (1.000) | 1.27 (1.000) | 0.00 (1.000) |
| 10 s | 0.00 | 0.00–0.00 | 0.88 (1.000) | 1.43 (1.000) | 0.51 (0.657) |
| 30 s | 1.00 | 0.00–3.00 | 0.84 (0.388) | 1.37 (0.706) | 2.44 (0.055) |

| Dispersion window | test | null block (p) | train |
|---|---|---|---|
| 1 min | 0.97 | 0.99 (1.000) | 1.02 |
| 5 min | 0.92 | 0.99 (0.940) | 1.07 |
| 10 min | 0.99 | 0.96 (0.413) | 1.04 |
| 30 min | 1.00 | 0.97 (0.378) | 0.92 |

- Inter-event gap CV (1 = Poisson), test: 0.85, null 0.85 (p 0.572); train 0.92
- Episodes (gap ≤ 30 s), test: 0 with ≥2 events; 0.0% of events in them (null 2.7%, p 1.000); median duration – s
- Pre-episode change on test, z over (-10, -2) s (n=50): det_max -0.1, det_mean -0.2, ctc_mean 0.3, inter_mean 0.5, cdc_sim_mean -0.5, disagree_mean 1.1, blank_mean 0.5, entropy_mean 0.9, rms_db_mean -0.6, in_clip_frac 2.8

**Evidence summary** (descriptive, not a formal test)

- ❌ 1. Test: clustering beyond conditions (RR 30 s > within-block null, p < 0.05)
- ❌ 2. Test: post-failure risk elevated (RR 30 s 95% CI above 1)
- ❌ 3. Train replicates it (RR 30 s > 1 and within-block p < 0.05)
- ❌ 4. Test: beyond speaker effects too (RR 30 s > within-speaker-run null, p < 0.05)
- ❌ 5. Test: elevated-risk periods last (episode share > null, duration > merge window)
- ❌ 6. Test: runtime signals change before episodes (|z| > 3 for entropy, blank or energy; n >= 10)

**0/6 → NO evidence of temporal structure beyond known conditions**

## 5.0 FA/h (threshold 0.9029)

Test: 143 events over 26.6 h. Train: 276 events over 58.1 h.

| Relative risk (L = H) | test | 95% CI | null block (p) | null run (p) | train (p block) |
|---|---|---|---|---|---|
| 5 s | 2.44 | 0.00–5.19 | 1.14 (0.090) | 1.73 (0.234) | 1.65 (0.219) |
| 10 s | 2.21 | 0.38–4.34 | 1.25 (0.055) | 1.79 (0.199) | 1.83 (0.075) |
| 30 s | 1.83 | 1.03–2.67 | 1.28 (0.045) | 1.65 (0.254) | 2.15 (0.005) |

| Dispersion window | test | null block (p) | train |
|---|---|---|---|
| 1 min | 1.02 | 1.02 (0.463) | 1.07 |
| 5 min | 1.02 | 1.09 (0.841) | 1.17 |
| 10 min | 1.05 | 1.07 (0.622) | 1.09 |
| 30 min | 1.11 | 1.12 (0.532) | 1.01 |

- Inter-event gap CV (1 = Poisson), test: 1.03, null 1.03 (p 0.507); train 1.10
- Episodes (gap ≤ 30 s), test: 8 with ≥2 events; 11.9% of events in them (null 10.4%, p 0.323); median duration 14.5 s
- Pre-episode change on test, z over (-10, -2) s (n=132): det_max 0.2, det_mean -0.2, ctc_mean 1.5, inter_mean 1.2, cdc_sim_mean -1.3, disagree_mean 1.8, blank_mean 1.4, entropy_mean 1.7, rms_db_mean 0.0, in_clip_frac 4.3

**Evidence summary** (descriptive, not a formal test)

- ✅ 1. Test: clustering beyond conditions (RR 30 s > within-block null, p < 0.05)
- ✅ 2. Test: post-failure risk elevated (RR 30 s 95% CI above 1)
- ✅ 3. Train replicates it (RR 30 s > 1 and within-block p < 0.05)
- ❌ 4. Test: beyond speaker effects too (RR 30 s > within-speaker-run null, p < 0.05)
- ❌ 5. Test: elevated-risk periods last (episode share > null, duration > merge window)
- ❌ 6. Test: runtime signals change before episodes (|z| > 3 for entropy, blank or energy; n >= 10)

**3/6 → PARTIAL evidence of temporal structure**

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
| 0.5 | dispersion 10 min vs within-block null | 0.313 | 1.000 | False |
| 0.5 | dispersion 30 min vs within-block null | 1.000 | 1.000 | False |
| 0.5 | gap CV vs within-block null | – | – | False |
| 0.5 | episode share vs within-block null | 1.000 | 1.000 | False |
| 1.0 | RR 5 s vs within-block null | 1.000 | 1.000 | False |
| 1.0 | RR 5 s vs within-run null | 1.000 | 1.000 | False |
| 1.0 | RR 10 s vs within-block null | 1.000 | 1.000 | False |
| 1.0 | RR 10 s vs within-run null | 1.000 | 1.000 | False |
| 1.0 | RR 30 s vs within-block null | 0.090 | 1.000 | False |
| 1.0 | RR 30 s vs within-run null | 0.229 | 1.000 | False |
| 1.0 | dispersion 1 min vs within-block null | 1.000 | 1.000 | False |
| 1.0 | dispersion 5 min vs within-block null | 0.781 | 1.000 | False |
| 1.0 | dispersion 10 min vs within-block null | 0.532 | 1.000 | False |
| 1.0 | dispersion 30 min vs within-block null | 1.000 | 1.000 | False |
| 1.0 | gap CV vs within-block null | 0.289 | 1.000 | False |
| 1.0 | episode share vs within-block null | 1.000 | 1.000 | False |
| 2.0 | RR 5 s vs within-block null | 1.000 | 1.000 | False |
| 2.0 | RR 5 s vs within-run null | 1.000 | 1.000 | False |
| 2.0 | RR 10 s vs within-block null | 1.000 | 1.000 | False |
| 2.0 | RR 10 s vs within-run null | 1.000 | 1.000 | False |
| 2.0 | RR 30 s vs within-block null | 0.388 | 1.000 | False |
| 2.0 | RR 30 s vs within-run null | 0.706 | 1.000 | False |
| 2.0 | dispersion 1 min vs within-block null | 1.000 | 1.000 | False |
| 2.0 | dispersion 5 min vs within-block null | 0.940 | 1.000 | False |
| 2.0 | dispersion 10 min vs within-block null | 0.413 | 1.000 | False |
| 2.0 | dispersion 30 min vs within-block null | 0.378 | 1.000 | False |
| 2.0 | gap CV vs within-block null | 0.572 | 1.000 | False |
| 2.0 | episode share vs within-block null | 1.000 | 1.000 | False |
| 5.0 | RR 5 s vs within-block null | 0.090 | 1.000 | False |
| 5.0 | RR 5 s vs within-run null | 0.234 | 1.000 | False |
| 5.0 | RR 10 s vs within-block null | 0.055 | 1.000 | False |
| 5.0 | RR 10 s vs within-run null | 0.199 | 1.000 | False |
| 5.0 | RR 30 s vs within-block null | 0.045 | 1.000 | True |
| 5.0 | RR 30 s vs within-run null | 0.254 | 1.000 | False |
| 5.0 | dispersion 1 min vs within-block null | 0.463 | 1.000 | False |
| 5.0 | dispersion 5 min vs within-block null | 0.841 | 1.000 | False |
| 5.0 | dispersion 10 min vs within-block null | 0.622 | 1.000 | False |
| 5.0 | dispersion 30 min vs within-block null | 0.532 | 1.000 | False |
| 5.0 | gap CV vs within-block null | 0.507 | 1.000 | False |
| 5.0 | episode share vs within-block null | 0.323 | 1.000 | False |

Stage 2 (`stage2_report.md`) runs whatever the outcome: a negative result, or states that only track SNR, is also a finding.

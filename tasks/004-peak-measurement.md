# 004: Measure peak height and width

- **Status:** active
- **Created:** 2026-11-22
- **Updated:** 2026-11-23
- **Due:** YYYY-MM-DD

## Goal

Every one of the 352 peaks (32 methods × 11 standards) has a height in counts and a full width at half maximum (FWHM) in min in a table in `analysis.ipynb`, each peak that cannot be trusted is flagged with the reason, and the measurements have been checked by eye against the raw chromatograms.

## Progress log

### 2026-11-22: raw chromatograms (Step 1)

- Plotted the slowest method (Method 22, iodododecane at 42.46 min) and the fastest (Method 3, iodododecane at 20.62 min) with the 11 listed retention times from `rts.csv`.
- Every listed retention time sits on a peak; the apex is within 0.012 min of the listed time.
- Peak heights differ about 30-fold between the two methods (Method 22: 0.4–1.5 × 10⁷ counts; Method 3: 0.6–4.2 × 10⁸ counts).
- Method 22 has large peaks between 5.04 and 6.95 min that are not standards, the largest 9.76 × 10⁸ counts at 5.61 min.
- In Method 3, iodopropane elutes at 4.19 min, 0.19 min after recording starts at 4.00 min, on the falling start of the trace.
- The baseline rises after the last standard (about 45 min in Method 22, 25 min in Method 3).

### 2026-11-22: peak measurement (Step 2)

- Window ±0.15 min around each listed retention time, straight baseline between the means of the first and last 5 points, FWHM from `scipy.signal.peak_widths`.
- Data used to set the window: FWHM 0.022–0.067 min; closest pair of standards 0.625 min apart (iodohexane and iodobenzene, Method 24); point spacing 0.0036 min.
- Changing the window from ±0.10 to ±0.25 min changes the median height and FWHM by less than 0.5 %.
- Results: height 2.7 × 10⁶ to 4.1 × 10⁸ counts; FWHM 0.022–0.067 min (1.3–4.0 s); 6–18 points across the FWHM.
- 12 of 352 peaks flagged: 4 windows start before the recording (iodopropane, Methods 12, 16, 20, 24); 6 change by more than 10 % with a ±0.25 min window (iodopropane, Methods 3, 7, 27; iodohexane, Methods 11, 25; iodobenzene, Method 31); 2 apexes more than 0.01 min from the listed time (iodoundecane, Method 9; iodododecane, Method 19).
- Plausibility: signal-to-noise median 800, minimum 20 (iodopropane, Methods 27 and 31); elution order the same in all 32 methods; one peak has a flat top.
- Committed as `0f1ed6c`.
- **Why I chose ±0.15 min and a straight baseline (my words):** ...

### 2026-11-22: peak check by eye, valley-to-valley baseline (Step 3)

- The check figure showed unlisted neighboring peaks inside the window for 17 peaks; window-edge baselines started on a neighbor's flank (iodohexane, Method 11: height 17 % too low).
- Changed to a valley-to-valley baseline and a half-height search between the valleys. Window-sensitive peaks: 6 → 0. Iodohexane, Method 11: 9.96 × 10⁷ → 1.17 × 10⁸ counts.
- Values of 10⁷ counts and above are stored rounded to 3 significant figures (91–99 % of them); the one flat-topped peak (iodobutane, Method 1) is rounding, not saturation.
- 20 of 352 peaks flagged; all measured correctly in the figure; kept.
- Committed as `fee78f6`.
- **Why I kept all flagged peaks (my words):** ...

### 2026-11-22: effects (Step 4)

- Design rebuilt from the data: A–E full 2⁵, F = ABC, G = ABDE, resolution IV; 31 contrasts (7 main, 18 two-factor-interaction columns, 6 higher-order).
- Effects on ln(height) and ln(FWHM) per standard. Median ratios high/low: B height ×9.9, F width ×0.64, G width ×1.17, A height ×0.72.
- Committed as `e207edc`.
- **Why a log scale (my words):** ...

### 2026-11-22: significance, Lenth's method (Step 5)

- α = 0.05; active above SME, possible between ME and SME.
- Height: B active 11/11, A and F 10/11, G 6/11. Width: B, F, G active 11/11. C and E never.
- Without the 20 flagged peaks: no height conclusion changes; iodopropane's width results are not robust.
- Committed as `76ab9c0`.
- **Why SME and not ME (my words):** ...

### 2026-11-22: early against late standards (Step 6)

- ln(late) − ln(early) per run, iodobutane–iodohexane against iododecane–iodododecane; slope over all 11 as a check.
- Height: A late/early 0.78 (active); D, F, G possible (active in the slope check). Width: B 1.12 and F 0.93 (active); F×G only on early peaks.
- Committed as `dc4dc19`.
- **Why I left iodopropane out of the early group (my words):** ...

### 2026-11-22: residuals (Step 7)

- Height residuals normal, but whole runs shift together (Methods 13, 17, 31: about −36 %, +47 %, −31 %); residual SD 0.227 against 0.166 expected from PSE. Width residual SD 0.044 against 0.036; long upper tail from tailing peaks (iodohexane, Methods 13 and 21).
- Committed as `4e5c37c`.
- **What I think causes the run shifts (my words):** ...

### 2026-11-23: factor names and conclusions (Step 8)

- Factor names from the figshare description order. Confirmed by retention time: B carrier flow, F ramp rate (low-F runs 63 min, high-F 41.5 min), G film thickness (iodopropane retention ×2.02). A, C, D, E by levels only.
- Open: split ratio (A) area ×0.69 and injection volume (D) area ×0.92 contradict the simple expectation (about ×0.06 and ×2).
- Draft conclusions added to the notebook, marked DRAFT.
- **Paper or mentor check of the A, C, D, E names:** ...
- **Conclusions rewritten in my own words:** (date) ...

## Outcome

...

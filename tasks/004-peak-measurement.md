# 004: Measure peak height and width

- **Status:** active
- **Created:** 2026-11-22
- **Updated:** 2026-11-22
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

## Outcome

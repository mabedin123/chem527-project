# Project proposal: Minhaj Ul Abedin

## Question
Which of the seven parameters significantly change peak width or height, and are they the same for early- and late-eluting standards?

## Data
Gamble, S.; Granger, C.; Mannion, J. *GC-MS Screening Data for Instrument Optimization*. figshare, 2025. https://doi.org/10.6084/m9.figshare.28635920.v1 (license GPL 3.0+). Accessed 2026-11-08. Associated article: *Anal. Chem.*, https://doi.org/10.1021/acs.analchem.3c05763.

The dataset holds 32 GC-MS total ion chromatograms of 11 iodinated standards, the design table, and the retention time of each standard in each method.

## Are the data sufficient?
Yes, the data is sufficient I have 32 runs * 11 peaks with 7 parameters at 2 levels, 11 standards and 352 peaks in total, 10325 to 16245 points per chromatogram. The columns I will use in my analysis are time_min, intensity counts, A-G and retention times. I have the settings for each run and the signal where each peak is. The chromatograms have a median of 11 and a minimum of 6 points across half height hence it would be sufficient to measure whether its a  narrow or wide peak. 

## What is missing, and what I would do if the data do not answer the question
There are no repeated runs which brings no possibility of viewing how the results vary by chance. To solve this I can use  a half normal plot to judge which effects stand out. There is also the problem of two setting interactions, some peaks are obscure such as the late peaks hard to measure and hence I plan to use only the clear peaks. The biggest problem of all is if no settings stand out or if the late peaks cannot be measured or unclear, then I will have to either report the early eluting standards or just conclude with that no parameter has a standing out effect. 

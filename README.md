# Reddit Headlines and Dow Volatility

Carnegie Mellon big-data coursework (spring 2025) by Pablo Zavala, MPP, testing whether
words in daily Reddit world-news headlines predict DJIA returns and volatility. The
committed notebook `dow_reddit_analysis.ipynb` is the original executed file with saved
outputs intact, so every headline number below stays checkable by reading the file
before running anything.

## What the notebook shows

- Across 3,183 filtered words (from 5,271 candidates) on 1,988 aligned trading days,
  marginal regressions give returns a flat, noise-like p-value histogram (121 words
  under p = 0.05) while volatility spikes near zero (272 words under p = 0.05).
- Benjamini-Hochberg FDR control at q = 0.1 keeps exactly one return word, "damn"
  (p = 1.0262e-05), which the notebook reads as minimal predictive ability rather
  than discovery; volatility keeps 12 words (cutoff p = 0.00035710), led by
  "tunisia", "georgia", and "terror".
- A words-only LassoCV (time-series split) zeroes every coefficient for both targets.
  Adding previous-day volatility yields six selected coefficients, in-sample R-squared
  0.262, and a persistence coefficient of 0.442; a double lasso against a union of
  1,429 selected word controls trims persistence from a naive 0.647 to 0.313
  (SE 0.0355, p = 1.6011e-17).
- A 30-resample bootstrap pins the cross-validated penalty at the 0.0001 grid floor
  with zero spread, a cautionary methods result about row resampling with
  cross-validation.

All evidence is in-sample, on one dataset whose newest DJIA date is July 1, 2016.

## A note on the saved run

The saved execution counts show the archived pass ran some cells out of order, so the
saved outputs reflect the last run of each cell rather than one top-to-bottom pass.
A clean rerun from the data download below makes the fair test.

## Data

The notebook reads four CSVs, all of which stay outside this repository for license
reasons:

- `RedditNews.csv` and `DJIA.csv`: from the Kaggle Daily News for Stock Market
  Prediction dataset (aaron7sun/stocknews).
- `WordsFinal.csv`: one word per row, the candidate vocabulary. Course-provided
  derived file (built from the Reddit headlines); available through the course
  rather than a public download.
- `WordFreqFinal.csv`: whitespace-delimited (day_index, word_index, count) triples
  aligned to the vocabulary and trading days. Same course-provided provenance.

A full rerun needs all four files in the repository root: the two Kaggle files
plus the two course-provided word files. Checking the quoted numbers needs zero
data: every figure appears in a saved cell output or the committed cell source.

## Author

Pablo Zavala (Carnegie Mellon University).

# Modeling I-95 Traffic Using Stochastic Probability Models

**STAT 422 — Probability Models | R / R Markdown**

**Authors:** Jihoon Lim, Achyutha Duddebanda, and Andrew Gaiano  
**Project type:** Undergraduate team project

## Overview

This project studies short-term traffic patterns on I-95 using minute-by-minute vehicle counts across four observation periods: Saturday morning, Saturday afternoon, Monday morning, and Monday afternoon. We apply three probability-modeling approaches to examine **traffic volume**, **changes in traffic states**, and **the proportion of trucks**.

The repository contains the original team's R Markdown analysis with descriptive summaries, model calculations, and visualizations.

## Methods

1. **Poisson model:** Estimate mean vehicle arrivals per minute (λ) for each observation period; compare observed vehicle-count frequencies with Poisson-model expectations.
2. **Discrete-time Markov chain:** Categorize traffic volume into Low, Medium, and High states using sample quantiles; estimate state-to-state transition probabilities and a stationary distribution from observed within-period transitions.
3. **Hierarchical Beta–Binomial model (empirical Bayes-style):** Estimate period-specific truck proportions with a shared beta prior centered on the overall truck rate; calculate posterior means and 95% credible intervals.

## Dataset and observations

The provided dataset contains **40 one-minute observations**, 10 for each period, with the columns `Date`, `Day`, `Time`, `Minute`, `Cars`, `Trucks`, and `Total`.

| Observation period | Minutes sampled | Mean vehicles / min | Total vehicles | Trucks (%) |
|---|---:|---:|---:|---:|
| Saturday AM | 10 | 22.0 | 220 | 6.8% |
| Saturday PM | 10 | 36.4 | 364 | 3.3% |
| Monday AM | 10 | 22.9 | 229 | 36.2% |
| Monday PM | 10 | 48.9 | 489 | 19.6% |

**Descriptive finding:** Monday PM had the highest observed mean traffic volume (**48.9 vehicles/minute**). The weekday and weekend differences are descriptive findings from this small sample, not general estimates for all I-95 traffic.

## Repository files

- [`I95_Traffic_Analysis.Rmd`](I95_Traffic_Analysis.Rmd) — analysis source, model explanations, code, and visualizations
- [`traffic.csv`](traffic.csv) — input workbook
- `README.md` — project overview and reproducibility instructions

## Reproduce the analysis

1. Install **R** and **RStudio** (or another editor capable of rendering R Markdown).
2. Open `I95_Traffic_Analysis.Rmd` in RStudio. Keep `traffic.csv` in the same working directory.
3. Install the required R packages (once):

   ```r
   install.packages(c("rmarkdown", "dplyr", "ggplot2", "knitr"))
   ```

4. Set the working directory to the repository folder (e.g. open the repository as an RStudio Project, or use `setwd()`), and select **Knit** to produce an HTML report.

   Alternatively, from that working directory:

   ```r
   rmarkdown::render("I95_Traffic_Analysis.Rmd")
   ```

The report reads `traffic.csv` from the current working directory (CSV version of the original Excel worksheet).

## Limitations

- Only 40 one-minute observations were analyzed; conclusions should not be generalized to I-95 as a whole.
- A homogeneous Poisson assumption and first-order Markov assumption may not capture all traffic dependencies; no formal validation of these assumptions is established here.
- The empirical Bayes-style beta prior uses a **chosen prior strength of 20** and is centered on the pooled truck proportion; the resulting intervals are conditional on that choice.
- The Markov stationary distribution is a modeled extrapolation, not directly observed long-run traffic behavior.

## Future improvements

Collect longer samples across more days, compare time-varying Poisson rates, validate state transitions on held-out periods, and examine the sensitivity of truck-rate estimates to prior choice.

## Attribution

This is a **team project** by the three authors listed above. Individual contributions are not specified in the original R Markdown file; please attribute individual work accurately when describing the project in applications or interviews.
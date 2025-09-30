# Sample Size Simulation for Hypothesis Testing

This repository contains an R script to simulate the effect of sample size on the probability of rejecting the null hypothesis in a one-sample t-test.

## Description

The simulation compares:

- **Type I error rate** when the null hypothesis is true.
- **Power** when a small effect exists (mean = 0.1).

The script generates a figure showing how increasing sample size affects the probability of rejecting the null hypothesis. A dashed line indicates the nominal 5% significance level.

## Requirements

- R >= 4.0
- ggplot2

Install ggplot2 if you don’t have it:

```r
install.packages("ggplot2")
```
## Usage

Run the R script:
source("sample_size_simulation.R")
The script will produce a plot with:
x-axis: Sample size (log scale)
y-axis: Probability of rejecting H0
Points and labels for rejection probabilities
A dashed line showing the nominal 5% significance level
Two scenarios: Null true and small effect

## Purpose
This simulation illustrates a common misconception: that simply increasing sample size increases the probability of rejecting the null hypothesis even when it is true. In fact, the Type I error remains controlled at the nominal level, while power increases for true effects.

## License
MIT License


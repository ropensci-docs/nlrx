# Backend function for collecting experiment metrics

Internal helper for combining regular metrics with turtle, patch and
link metrics.

## Usage

``` r
util_collect_experiment_metrics(nl)
```

## Arguments

- nl:

  nl object

## Value

character vector of NetLogo reporter metrics

## Details

Combines regular experiment metrics with additional agent metrics
defined in `metrics.turtles`, `metrics.patches` and `metrics.links`.

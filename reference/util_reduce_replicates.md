# Reduce replicated simulation results to one value per metric

Aggregate simulation results over measured ticks and over replicates

## Usage

``` r
util_reduce_replicates(results, cols)
```

## Arguments

- results:

  tibble of simulation results, as returned by
  [`run_nl_one()`](https://docs.ropensci.org/nlrx/reference/run_nl_one.md)

- cols:

  character vector of metric columns that should be reduced

## Value

tibble with one row and one column per entry of `cols`

## Details

Reduction happens in two stages: first the mean over all measured ticks
within each replicate, then the mean over the replicates. Replicates are
identified by the `random-seed` column. The two stages matter whenever
replicates return a different number of ticks (for example when an exit
condition is defined), because a single mean over all rows would weight
long runs higher than short ones.

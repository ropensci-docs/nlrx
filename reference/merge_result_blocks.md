# Backend function for `run_nl_all()`

Merges results produced by
[`run_nl_block()`](https://docs.ropensci.org/nlrx/reference/run_nl_block.md)
into one tibble. Temporarily handles column name restoration until
`logolink` supports preserving original column names.

## Usage

``` r
merge_result_blocks(nl, results_list)
```

## Arguments

- nl:

  See
  [`run_nl_all()`](https://docs.ropensci.org/nlrx/reference/run_nl_all.md)

- results_list:

  List of result tibbles returned by
  [`run_nl_block()`](https://docs.ropensci.org/nlrx/reference/run_nl_block.md)

## Value

Tibble with simulation output results

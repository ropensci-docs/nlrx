# Backend function used by `run_nl_all()` and `run_nl_one()` to run simulations (NetLogo 7+)

Creates a BehaviorSpace XML file for simulations defined in `block_df`
and executes them via `logolink`

## Usage

``` r
run_nl_block(nl, block_df, block_number, threads)
```

## Arguments

- nl:

  See
  [`run_nl_all()`](https://docs.ropensci.org/nlrx/reference/run_nl_all.md)

- block_df:

  Data frame of simulation definitions, with one row being one run

- block_number:

  Assigned by
  [`run_nl_all()`](https://docs.ropensci.org/nlrx/reference/run_nl_all.md),
  used for naming the XML file.

## Value

Tibble with simulation output results

## Details

Runs a single block (`block_df`) by writing a single BehaviorSpace XML
file and executing it via `logolink`.

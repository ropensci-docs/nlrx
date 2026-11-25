# Backend function for `run_nl_all()` (NetLogo 7+)

Splits `nl@simdesign@siminput` into blocks of size `block_size`, to be
executed by
[`run_nl_block()`](https://docs.ropensci.org/nlrx/reference/run_nl_block.md)

## Usage

``` r
create_simulation_blocks(nl, block_size)
```

## Arguments

- nl:

  See
  [`run_nl_all()`](https://docs.ropensci.org/nlrx/reference/run_nl_all.md)

- block_size:

  See
  [`run_nl_all()`](https://docs.ropensci.org/nlrx/reference/run_nl_all.md)

## Value

A list of data frames, each representing one bundle of simulations

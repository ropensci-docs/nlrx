# Run one evaluation of a dynamic simdesign

Runs the simulations of one evaluation via
[`run_nl_one()`](https://docs.ropensci.org/nlrx/reference/run_nl_one.md),
without its console output, and advances the progress bar of
[`run_nl_dyn()`](https://docs.ropensci.org/nlrx/reference/run_nl_dyn.md).

## Usage

``` r
util_run_nl_dyn_evaluation(nl, seed, threads = 1)
```

## Arguments

- nl:

  nl object with the parameterisation of this evaluation as siminput

- seed:

  vector of model seeds, one per replicated run of this evaluation

- threads:

  number of NetLogo threads used for execution (handled via NetLogo).

## Value

Tibble with simulation output results

## Details

An optimization runs thousands of evaluations, so the messages of each
run (BehaviorSpace XML path, NetLogo progress) are held back. They are
shown when the run fails, together with the error.

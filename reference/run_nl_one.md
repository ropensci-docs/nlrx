# Execute one NetLogo simulation from a nl object

Execute one NetLogo simulation from a nl object with a defined
experiment and simdesign

## Usage

``` r
run_nl_one(nl, seed, threads = 1, siminputrow, ...)
```

## Arguments

- nl:

  nl object

- seed:

  a random seed for the NetLogo simulation, or a vector of random seeds
  to run the same parameterisation repeatedly

- threads:

  number of NetLogo threads used for execution (handled via NetLogo).

- siminputrow:

  rownumber of the input tibble within the attached simdesign object
  that should be executed

- ...:

  additional arguments; currently only used to detect and warn about
  arguments that were deprecated in earlier nlrx versions.

## Value

tibble with simulation output results

## Details

Uses the `logolink` backend for NetLogo 7+. `run_nl_one()` executes one
simulation of the specified NetLogo model within the provided nl object.
The random seed is set within the NetLogo model to control
stochasticity. For further information, see the Reproducibility section
in
[`run_nl_all()`](https://docs.ropensci.org/nlrx/reference/run_nl_all.md).
The siminputrow number defines which row of the input data tibble within
the simdesign object of the provided nl object is executed.

If `seed` is a vector of more than one seed, the same parameterisation
is executed once per seed. These replicated runs are independent of each
other, and each of them reports its own seed in the `random-seed` column
of the results.

The `threads` argument controls NetLogo's native multithreading. This is
relevant when more than one seed is executed, because the runs are then
parallelized within one NetLogo instance. For a single run, `threads`
has no effect.

## Suppressing Messages

Informational messages (e.g., XML file paths) are displayed using the
`cli` package. To suppress these messages, wrap the function call with
[`suppressMessages()`](https://rdrr.io/r/base/message.html), e.g.,
`suppressMessages(run_nl_one(nl, 123, 1))`.

## Examples

``` r
if (FALSE) { # \dontrun{

# Load nl object from test data:
nl <- nl_lhs

# Run one simulation:
results <- run_nl_one(nl = nl,
                      seed = getsim(nl, "simseeds")[1],
                      siminputrow = 1)

# Run the same parameterisation with three different seeds:
results <- run_nl_one(nl = nl,
                      seed = getsim(nl, "simseeds")[1:3],
                      siminputrow = 1)

} # }
```

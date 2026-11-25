# Execute all NetLogo simulations from a nl object

Execute all NetLogo simulations from a nl object with a defined
experiment and simdesign

## Usage

``` r
run_nl_all(nl, block_size = 100, threads = 1, ...)
```

## Arguments

- nl:

  nl object

- block_size:

  number of simulations bundled into one execution block (one NetLogo
  instance can only receive one block).

- threads:

  number of NetLogo threads used for execution (handled via NetLogo).

- ...:

  additional arguments; currently only used to detect and warn about
  arguments that were deprecated in earlier nlrx versions.

## Value

tibble with simulation output results

## Details

run_nl_all executes all simulations of the specified NetLogo model
within the provided nl object.

The function structures the simdesign table into blocks, sized via
`block_size`. Each block is passed to `logolink`, which writes a
BehaviorSpace XML file and executes it.

Multithreading is supported via NetLogo natively, and controlled using
`threads`. See how many threads you can assign using
[`parallel::detectCores()`](https://rdrr.io/r/parallel/detectCores.html).

Progress can be shown by wrapping run_nl_all() with `progressr` (see
examples). Progress updates on completion of one block.

Small `block_size` results in frequent updates of simulation status, but
causes simulations to take longer, as NetLogo has to restart after every
block. Large `block_size` results in infrequent updates but will
generally be faster (although with rapidly diminishing returns).

### Debugging:

Make sure you can run your NetLogo model on your machine. Make sure that
Java is installed and available from the terminal (java -version). Use
`eval_variables_constants(nl)` to check the validity of model settings.
Lastly, the R console outputs XML filepaths. These XML files are
`BehaviorSpace` definitions. Run these manually via NetLogo
`BehaviorSpace` to diagnose issues with the experiment and simdesign
setup.

## Reproducibility and Seeds

Every simulation is executed with an explicit random seed, taken from
the `nseeds` seeds of the attached simdesign (`nl@simdesign@simseeds`).
NetLogo is seeded with that value and reports it back, so each row of
the results can be traced to the parameterisation (`siminputrow`) and
the seed (`random-seed`) that produced it. Re-running a design with the
same seeds therefore reproduces the results exactly. To replicate a
parameterisation under different stochasticity, increase `nseeds` in the
simdesign helper.

## Suppressing Messages

Informational messages (e.g., XML file paths) are displayed using the
`cli` package. To suppress these messages, wrap the function call with
[`suppressMessages()`](https://rdrr.io/r/base/message.html), e.g.,
`suppressMessages(run_nl_all(nl))`.

## Examples

``` r
if (FALSE) { # \dontrun{

# Load nl object from test data:
nl <- nl_lhs

# Execute all simulations from an nl object with properly attached simdesign.
results <- run_nl_all(nl)

# Run in parallel on local machine (NetLogo 7+):
library(progressr)
with_progress({ # progress bar
results <- run_nl_all(nl, threads = 10) # 10 threads
})

# Adjust block size for performance tuning:
# Larger block_size means fewer NetLogo restarts (re-initialized once per block):
results <- run_nl_all(nl, block_size = 500, threads = 10)
} # }
```

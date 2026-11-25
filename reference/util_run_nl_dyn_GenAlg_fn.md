# Genetic Algorithm run simulation function

Genetic Algorithm run simulation function

Genetic Algorithm run simulation function

## Usage

``` r
util_run_nl_dyn_GenAlg_fn(param, nl, evalcrit, seed, threads = 1, ...)

util_run_nl_dyn_ABCmcmc_fn(param, threads = 1)
```

## Arguments

- param:

  vector of model parameters passed from ABC_mcmc function. If use_seeds
  = TRUE, the first element of this vector is a random seed

- nl:

  nl object

- evalcrit:

  evaluation criterion for simulated annealing

- seed:

  vector of model seeds, one per replicated run of this evaluation

- threads:

  number of NetLogo threads used for execution (handled via NetLogo).

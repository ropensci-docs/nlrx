# Report the evaluation budget of a dynamic simdesign

Tells how many evaluations (NetLogo runs) the optimization of each seed
may take, and which arguments control that number.

## Usage

``` r
util_report_dyn_budget(nl, nseeds, nreplicates)
```

## Arguments

- nl:

  nl object with a GenSA, GenAlg or ABCmcmc simdesign

- nseeds:

  number of seeds, i.e. optimizations

- nreplicates:

  number of replicated runs per evaluation

## Value

The (approximate) maximum number of evaluations per seed, NA if unknown,
invisibly.

## Details

A GenSA simdesign without any stop criterion in `control` (`max.call`,
`max.time`, `maxit`, `nb.stop.improvement` or `threshold.stop`) runs
with the GenSA defaults (`maxit = 5000`, `max.call = 1e7`), which take
tens of thousands of evaluations; this is reported as a warning.

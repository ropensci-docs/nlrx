# Identify evalticks without results

Reports the evalticks of an experiment for which no simulation records
were returned

## Usage

``` r
util_unreported_evalticks(evalticks, steps)
```

## Arguments

- evalticks:

  the `evalticks` of the experiment

- steps:

  the tick numbers present in the simulation results

## Value

the requested evalticks that are missing from `steps`, in the order
given

## Details

Simulations can end before a requested tick is reached, either because
`runtime` is shorter or because a `stopcond` ended them. The affected
ticks then silently carry no results, which this function surfaces.

# Check the calibration step of an ABC-MCMC simdesign

Stops if the calibration step keeps fewer than two runs, from which
EasyABC cannot derive the proposal range of the MCMC.

## Usage

``` r
util_eval_abc_calibration(n_calibration, tolerance_quantile)
```

## Arguments

- n_calibration:

  number of simulations of the calibration step

- tolerance_quantile:

  share of the calibration simulations that is kept

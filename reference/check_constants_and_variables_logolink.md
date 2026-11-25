# Backend function for eval_variables_constants (NetLogo 7+)

Checks constants and variable formatting of the experiment as required
by Logolink

## Usage

``` r
check_constants_and_variables_logolink(nl)
```

## Arguments

- nl:

  nl object

## Value

Character vector of detected issues

## Details

Checks constants and variable formatting of the experiment, as NetLogo
7+ (or at least Logolink) has different formatting specifications than
before.

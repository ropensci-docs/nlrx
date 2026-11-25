# Collapse NetLogo commands into one code block

Turns an experiment slot that may hold several procedures or commands
into one string

## Usage

``` r
util_collapse_commands(commands)
```

## Arguments

- commands:

  character vector of NetLogo procedures or commands, possibly NA

## Value

a single character string, or NULL if nothing is defined

## Details

`idsetup`, `idgo`, `idfinal` and `stopcond` accept a vector, which
NetLogo expects as one block of code with one command per line. Returns
NULL for an undefined slot, which is what 'logolink' expects for "not
set".

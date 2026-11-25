# Read NetLogo behavior space experiments from files

Read NetLogo behavior space experiments from files

## Usage

``` r
nldoc_table_bs(modelfiles)
```

## Arguments

- modelfiles:

  vector of filepaths to model files

## Value

list containing NetLogo behavior space experiments

## Details

The procedure reads the behavior space experiments of the main model
file (.nlogox) and reports one list per experiment: its `name`, the
`definitions` (procedures, time limit, metrics, ...) as a named
character vector, the `parameters` (constants) and the parameter sets of
its `subexperiments` as tibbles with the columns name, type and values.

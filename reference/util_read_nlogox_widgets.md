# Read the parameter widgets of a NetLogo 7 model

Reads the sliders, switches, input boxes and choosers of a .nlogox model
file.

## Usage

``` r
util_read_nlogox_widgets(modelpath)
```

## Arguments

- modelpath:

  Path to a .nlogox model file

## Value

named list with one entry per widget (type, value and the properties of
the widget type), or NULL if the model has no widgets block

## Details

Used by
[`report_model_parameters()`](https://docs.ropensci.org/nlrx/reference/report_model_parameters.md)
and [`nldoc()`](https://docs.ropensci.org/nlrx/reference/nldoc.md).

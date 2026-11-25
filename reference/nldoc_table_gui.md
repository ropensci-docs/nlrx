# Read NetLogo GUI elements from files

Read NetLogo GUI elements from files

## Usage

``` r
nldoc_table_gui(modelfiles)
```

## Arguments

- modelfiles:

  vector of filepaths to model files

## Value

list containing NetLogo GUI elements, or NA if the model has none

## Details

The procedure reads the parameter widgets (sliders, switches, input
boxes and choosers) of the main model file (.nlogox) and reports a list
of GUI elements.

# Reject NetLogo 6 model files

Stops with an advice-style error if any of the model files is in the
NetLogo 6 format (.nlogo).

## Usage

``` r
util_check_model_format(modelpath)
```

## Arguments

- modelpath:

  Character vector of model file paths. An empty vector passes, so an nl
  object can be created before the model is known.

## Details

NetLogo 7 converts .nlogo files when it opens them, so a .nlogo model
would even run. nlrx itself cannot read the old format (parameter
reports, variable checks, nldoc), and the conversion is meant as a
deliberate step, so the user is asked to convert the model once in
NetLogo 7.

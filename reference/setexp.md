# Setter function to set a variable of an experiment object

Setter function to set a variable of an experiment object

## Usage

``` r
setexp(nl, var) <- value
```

## Arguments

- nl:

  nl object

- var:

  valid experiment variable string

- value:

  valid value for the specified variable

## Examples

``` r

# Example for Wolf Sheep Predation model from NetLogo models library:
nl <- nl(nlversion = "7.0.4",
nlpath = "/home/user/NetLogo 7.0.4/",
modelpath = "/home/user/NetLogo 7.0.4/models/Sample Models/Biology/Wolf Sheep Predation.nlogox",
jvmmem = 1024)

# Set experiment name
setexp(nl, "expname") <- "experimentName"
```

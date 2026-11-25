# Getter function to get a variable of a nl object

Getter function to get a variable of a nl object

## Usage

``` r
getnl(nl, var)
```

## Arguments

- nl:

  nl object

- var:

  valid nl variable string

## Examples

``` r

# Example for Wolf Sheep Predation model from NetLogo models library:
nl <- nl(nlversion = "7.0.4",
nlpath = "/home/user/NetLogo 7.0.4/",
modelpath = "/home/user/NetLogo 7.0.4/models/Sample Models/Biology/Wolf Sheep Predation.nlogox",
jvmmem = 1024)

# get NetLogo version
getnl(nl, "nlversion")
#> [1] "7.0.4"
```

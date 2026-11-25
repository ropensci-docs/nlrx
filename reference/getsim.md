# Getter function to get a variable of a simdesign object

Getter function to get a variable of a simdesign object

## Usage

``` r
getsim(nl, var)
```

## Arguments

- nl:

  nl object

- var:

  valid simdesign variable string

## Examples

``` r
# Example for Wolf Sheep Predation model from NetLogo models library:
nl <- nl(nlversion = "7.0.4",
nlpath = "/home/user/NetLogo 7.0.4/",
modelpath = "/home/user/NetLogo 7.0.4/models/Sample Models/Biology/Wolf Sheep Predation.nlogox",
jvmmem = 1024)

# Set simulation seeds
setsim(nl, "simseeds") <- c(123, 456, 789)

# Set simulation seeds
getsim(nl, "simseeds")
#> [1] 123 456 789
```

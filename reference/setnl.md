# Setter function to set a variable of a nl object

Setter function to set a variable of a nl object

## Usage

``` r
setnl(nl, var) <- value
```

## Arguments

- nl:

  nl object

- var:

  valid nl variable string

- value:

  valid value for the specified variable

## Examples

``` r
# Example for Wolf Sheep Predation model from NetLogo models library:
nl <- nl(
nlpath = "/home/user/NetLogo 7.0.4/",
modelpath = "/home/user/NetLogo 7.0.4/models/Sample Models/Biology/Wolf Sheep Predation.nlogox",
jvmmem = 1024)

# set NetLogo version
setnl(nl, "nlversion") <- "7.0.4"
```

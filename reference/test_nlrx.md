# Test if nlrx runs on the local system

Runs a short test if nlrx runs on the local system

## Usage

``` r
test_nlrx(nlpath, nlversion)
```

## Arguments

- nlpath:

  Provide a path to a netlogo folder

- nlversion:

  Matching version string of the provided NetLogo folder (e.g. "7.0.4")

## Details

Runs a short test if nlrx runs on the local system. Reports TRUE if
successful!

## Examples

``` r
if (FALSE) { # \dontrun{
test_nlrx(nlpath="/Users/xyz/netlogo/NetLogo 7.0.4", nlversion="7.0.4")
} # }
```

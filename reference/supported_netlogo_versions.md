# Report tested NetLogo versions

Auxiliary function to report the NetLogo versions nlrx is tested with

## Usage

``` r
supported_netlogo_versions()
```

## Value

a vector of NetLogo versions that nlrx is tested with (parameter
`version`)

## Details

These are the versions used in the automated tests and for
[download_netlogo](https://docs.ropensci.org/nlrx/reference/download_netlogo.md).
Newer NetLogo 7 releases are not rejected: because execution is
delegated to 'logolink', they are likely to work and only emit a warning
(see
[check_netlogo_version](https://docs.ropensci.org/nlrx/reference/check_netlogo_version.md)).

## Examples

``` r
if (FALSE) { # \dontrun{
supported_netlogo_versions()
} # }
```

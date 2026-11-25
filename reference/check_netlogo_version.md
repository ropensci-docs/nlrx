# Check NetLogo versions

Auxiliary function to check a NetLogo version number against the tested
versions

## Usage

``` r
check_netlogo_version(version, throw_error = FALSE)
```

## Arguments

- version:

  Character string naming which NetLogo Version to check

- throw_error:

  TRUE/FALSE, if TRUE untested versions are reported (see details)

## Value

logical, TRUE if the version is one of
[supported_netlogo_versions](https://docs.ropensci.org/nlrx/reference/supported_netlogo_versions.md)

## Details

With `throw_error = TRUE` a version that is not among the tested ones is
reported according to how likely it is to work:

- NetLogo **7.0.0 or newer**: a **warning**. Simulations are executed by
  'logolink', so untested releases are likely to run; set
  `check_version = FALSE` in
  [nl](https://docs.ropensci.org/nlrx/reference/nl.md) to silence it.

- NetLogo **below 7.0.0**: an **error**. Support for these versions was
  removed in nlrx 0.5.0, so simulations cannot run at all. The error
  points to nlrx 0.4.6, the last version supporting NetLogo 5.3.1 to
  6.4.0, which can be installed from GitHub with
  `remotes::install_github("ropensci/nlrx@v0.4.6")`.

- A string that is not a version number: an **error**.

## Examples

``` r
if (FALSE) { # \dontrun{
check_netlogo_version("7.0.0")
check_netlogo_version("1.0")
check_netlogo_version("1.0", TRUE)
} # }
```

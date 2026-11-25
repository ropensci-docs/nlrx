# Report a NetLogo version that nlrx is not tested with

Signals the advice-style error or warning for a NetLogo version that is
not among
[supported_netlogo_versions](https://docs.ropensci.org/nlrx/reference/supported_netlogo_versions.md)
(see
[check_netlogo_version](https://docs.ropensci.org/nlrx/reference/check_netlogo_version.md)
for the rules).

## Usage

``` r
util_report_netlogo_version(version, in_nl = FALSE)
```

## Arguments

- version:

  Character string naming the NetLogo version

- in_nl:

  TRUE if called from
  [`nl()`](https://docs.ropensci.org/nlrx/reference/nl.md), which adds
  the hint how to silence the warning for untested NetLogo 7 versions

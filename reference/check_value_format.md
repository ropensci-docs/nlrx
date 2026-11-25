# Helper function for `check_constants_and_variables_logolink()`

Checks variables and constants for value patterns that nlrx cannot
repair

## Usage

``` r
check_value_format(x, name = NULL)
```

## Arguments

- x:

  value to check

- name:

  optional name of the checked entry

## Value

Character vector of detected issues

## Details

Escaped string quotes and boolean strings are normalized by
[util_normalize_nl_value](https://docs.ropensci.org/nlrx/reference/util_normalize_nl_value.md)
and are not reported here. What remains are values that cannot survive
the handover to 'logolink' at all: it quotes every character value, so
NetLogo literals such as `"[1 2 3]"` would be passed to the model as a
string.

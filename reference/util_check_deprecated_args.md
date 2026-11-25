# Utility function for checking for deprecated or unsupported arguments

Utility function for checking for deprecated or unsupported arguments

## Usage

``` r
util_check_deprecated_args(dots, deprecated_args)
```

## Arguments

- dots:

  Named list of arguments captured from `...`

- deprecated_args:

  Character vector of deprecated argument names that should trigger
  depreciation warnings (and not errors)

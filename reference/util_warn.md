# Signal a warning with an advice-style message

Warning counterpart of
[`util_abort()`](https://docs.ropensci.org/nlrx/reference/util_abort.md).

## Usage

``` r
util_warn(message, class = NULL, .envir = parent.frame())
```

## Arguments

- message:

  Character vector, formatted with
  [`cli::format_warning()`](https://cli.r-lib.org/reference/format_error.html)
  (see
  [`util_abort()`](https://docs.ropensci.org/nlrx/reference/util_abort.md)).

- class:

  Character vector of condition classes, prepended to `"nlrx_warning"`.

- .envir:

  Environment in which the message is interpolated.

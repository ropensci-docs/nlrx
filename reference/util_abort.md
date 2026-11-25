# Signal an error with an advice-style message

Signal an error for a problem in the user's setup (wrong NetLogo
version, wrong model format, ...) that the user can fix.

## Usage

``` r
util_abort(message, class = NULL, .envir = parent.frame())
```

## Arguments

- message:

  Character vector, formatted with
  [`cli::format_error()`](https://cli.r-lib.org/reference/format_error.html).
  Unnamed elements state the problem, `"i"` elements give context and
  `">"` elements say what to do. cli inline markup and glue
  interpolation are evaluated in `.envir`.

- class:

  Character vector of condition classes, prepended to `"nlrx_error"`.

- .envir:

  Environment in which the message is interpolated.

## Details

The condition is a base R error without a call, so neither the call nor
a backtrace is printed - the user sees the advice only. Genuine runtime
failures (NetLogo errors, internal errors) keep using
[`stop()`](https://rdrr.io/r/base/stop.html).

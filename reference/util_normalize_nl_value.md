# Normalize parameter values for the logolink backend

Repairs the two value conventions of nlrx \< 0.5.0 that are no longer
valid now that 'logolink' writes the BehaviorSpace XML: strings that
were wrapped in escaped quotes and booleans that were given as character
strings.

## Usage

``` r
util_normalize_nl_value(x)
```

## Arguments

- x:

  value or vector of values of a single NetLogo global

## Value

`x` with legacy quoting and boolean strings normalized

## Details

'logolink' quotes character values itself and lowercases logical values,
so a value like `"\"default\""` would reach NetLogo as `""default""` and
abort the run, and a value like `"false"` would reach it as the string
`"false"` instead of a boolean.

One layer of enclosing double quotes is therefore removed, and character
values that are entirely `"true"`/`"false"` (in any capitalisation) are
converted to logical. This also applies to a quoted `"\"true\""`:
NetLogo parses an unquoted `true` as a boolean, so a global whose value
is the *string* "true" could not be expressed before 0.5.0 either.

Values that are not character (numbers, logicals, stepped value lists)
are returned unchanged. The function is idempotent, so it can be applied
at several points of the pipeline.

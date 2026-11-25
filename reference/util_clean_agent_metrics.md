# Backend function for cleaning agent metrics

Internal helper for formatting turtle, patch and link metrics in
simulation output.

## Usage

``` r
util_clean_agent_metrics(NLtable, nl, expect_cleaned_names = FALSE)
```

## Arguments

- NLtable:

  simulation output table

- nl:

  nl object

- expect_cleaned_names:

  TRUE/FALSE, if TRUE reporter column names are expected to be cleaned
  by
  [`janitor::make_clean_names()`](https://sfirke.github.io/janitor/reference/make_clean_names.html).

## Value

simulation output table with cleaned agent metrics

## Details

Converts raw turtle, patch and link metric reporter output into nested
output columns.

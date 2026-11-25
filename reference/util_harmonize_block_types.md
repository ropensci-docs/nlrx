# Harmonize result column types across simulation blocks

Makes columns that have different types in different blocks bindable

## Usage

``` r
util_harmonize_block_types(results_list)
```

## Arguments

- results_list:

  list of result tibbles, one per simulation block

## Value

`results_list` with conflicting columns converted to character

## Details

A metric can come back as a number in one block and as a character in
another, for example when a run reports a NetLogo error message. Binding
the blocks then fails and the results of all completed runs are lost.
Such columns are converted to character in every block instead, with a
warning naming them. List columns (agent metrics) are left untouched.

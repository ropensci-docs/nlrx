# Analyze NetLogo simulation output

Analyze NetLogo simulation output

## Usage

``` r
analyze_nl(nl, metrics = getexp(nl, "metrics"), funs = list(mean = mean))
```

## Arguments

- nl:

  nl object

- metrics:

  vector of strings defining metric columns for evaluation. Defaults to
  metrics of the experiment within the nl object

- funs:

  list with the summary metrics for the sensitivity results

## Value

analysis summary tibble

## Details

The analyze_nl function runs basic analyses on NetLogo simulation
output. In order to execute this function, simulation output needs to be
attached to the simdesign first with `setsim(nl, "output") <- results`.

analyze_nl calls different post-processing analysis functions, depending
on the specified method in the simdesign object of the nl object.

**The following simdesign are currently supported:**

[simdesign_ff](https://docs.ropensci.org/nlrx/reference/simdesign_ff.md)

Calls
[analyze_ff](https://docs.ropensci.org/nlrx/reference/analyze_ff.md).
The function calculates aggregated output metrics by dropping random
seeds and aggregating values with the provided functions.

[simdesign_lhs](https://docs.ropensci.org/nlrx/reference/simdesign_lhs.md)

Calls
[analyze_lhs](https://docs.ropensci.org/nlrx/reference/analyze_lhs.md).
The function calculates aggregated output metrics by dropping random
seeds and aggregating values with the provided functions.

[simdesign_sobol](https://docs.ropensci.org/nlrx/reference/simdesign_sobol.md)

Calls
[analyze_sobol](https://docs.ropensci.org/nlrx/reference/analyze_sobol.md).
The function calculates sobol sensitivity indices from the output
results using the
[sensitivity](https://rdrr.io/pkg/sensitivity/man/sensitivity-package.html)
package.

[simdesign_sobol2007](https://docs.ropensci.org/nlrx/reference/simdesign_sobol2007.md)

Calls
[analyze_sobol2007](https://docs.ropensci.org/nlrx/reference/analyze_sobol2007.md).
The function calculates sobol sensitivity indices from the output
results using the
[sensitivity](https://rdrr.io/pkg/sensitivity/man/sensitivity-package.html)
package.

[simdesign_soboljansen](https://docs.ropensci.org/nlrx/reference/simdesign_soboljansen.md)

Calls
[analyze_soboljansen](https://docs.ropensci.org/nlrx/reference/analyze_soboljansen.md).
The function calculates sobol sensitivity indices from the output
results using the
[sensitivity](https://rdrr.io/pkg/sensitivity/man/sensitivity-package.html)
package.

[simdesign_morris](https://docs.ropensci.org/nlrx/reference/simdesign_morris.md)

Calls
[analyze_morris](https://docs.ropensci.org/nlrx/reference/analyze_morris.md).
The function calculates morris sensitivity indices from the output
results using the
[sensitivity](https://rdrr.io/pkg/sensitivity/man/sensitivity-package.html)
package.

[simdesign_eFast](https://docs.ropensci.org/nlrx/reference/simdesign_eFast.md)

Calls
[analyze_eFast](https://docs.ropensci.org/nlrx/reference/analyze_eFast.md).
The function calculates eFast sensitivity indices from the output
results using the
[sensitivity](https://rdrr.io/pkg/sensitivity/man/sensitivity-package.html)
package.

**For the following simdesign no postprocessing analysis function has
been implemented yet:**

[simdesign_simple](https://docs.ropensci.org/nlrx/reference/simdesign_simple.md),
[simdesign_distinct](https://docs.ropensci.org/nlrx/reference/simdesign_distinct.md),
[simdesign_GenSA](https://docs.ropensci.org/nlrx/reference/simdesign_GenSA.md),
[simdesign_GenAlg](https://docs.ropensci.org/nlrx/reference/simdesign_GenAlg.md)

## Examples

``` r

# Load nl object including output data from testdata
nl <- nl_sobol

# Define aggregation measurements:
myfuns <- list(mean=mean, sd=sd, min=min, max=max)

# Calculate sensitivity indices:
analyze_nl(nl, funs = myfuns)
#> [1] "No missing combinations detected!"
#> # A tibble: 18 × 8
#>    original    bias `std. error` `min. c.i.` `max. c.i.` parameter metric   seed
#>       <dbl>   <dbl>        <dbl>       <dbl>       <dbl> <chr>     <chr>   <dbl>
#>  1    0.936 0.00937       0.0776     0.759         1     initial-… count… 1.05e9
#>  2    0.193 0.00521       0.154      0             0.522 initial-… count… 1.05e9
#>  3    0     0             0.188      0             0.204 initial-… count… 1.05e9
#>  4    0     0             0.144      0             0.192 initial-… count… 1.05e9
#>  5    0.802 0.00504       0.0450     0.707         0.881 initial-… count… 1.05e9
#>  6    0.333 0.0226        0.161      0.00820       0.658 initial-… count… 1.05e9
#>  7    0.936 0.00586       0.0855     0.764         1     initial-… count… 1.05e9
#>  8    0.193 0.0183        0.135      0             0.450 initial-… count… 1.05e9
#>  9    0     0             0.175      0             0.275 initial-… count… 1.05e9
#> 10    0     0.0111        0.167      0             0.175 initial-… count… 1.05e9
#> 11    0.802 0.00610       0.0548     0.690         0.905 initial-… count… 1.05e9
#> 12    0.333 0             0.187      0             0.781 initial-… count… 1.05e9
#> 13    0.936 0             0.0777     0.784         1     initial-… count… 1.05e9
#> 14    0.193 0.0363        0.150      0             0.455 initial-… count… 1.05e9
#> 15    0     0             0.183      0             0.310 initial-… count… 1.05e9
#> 16    0     0.00481       0.169      0             0.184 initial-… count… 1.05e9
#> 17    0.802 0             0.0467     0.706         0.888 initial-… count… 1.05e9
#> 18    0.333 0             0.186      0             0.680 initial-… count… 1.05e9
```

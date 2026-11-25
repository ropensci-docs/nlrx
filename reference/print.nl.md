# Print content of nl object

Print content of nl object and embedded experiment and simdesign objects
to console

## Usage

``` r
# S3 method for class 'nl'
print(x, ...)
```

## Arguments

- x:

  nl object to print

- ...:

  further arguments passed to or from other methods

## Details

Print content of the provided nl object in a readable format.

## Examples

``` r

print(nl_lhs)
#> 
#>    NL OBJECT   
#> NetLogo version = 7.0.4
#> NetLogo path    = C:/Program Files/NetLogo 7.0.4/
#> Model path      = C:/Program Files/NetLogo 7.0.4/models/Sample Models/Biology/Wolf Sheep Predation.nlogox
#> JVM memory      = 1000
#> 
#>    EXPERIMENT   
#> Experiment name        = nlrx
#> Output path            = C:/out
#> Measure on each tick?  = false
#> Setup procedure(s)     = setup
#> Go procedure(s)        = go
#> Final procedure(s)     = NA
#> Run nr. widget name    = NA
#> Runtime (ticks)        = 10
#> Report output on ticks = 10
#> Stop condition         = NA
#> Metrics (output)       = count sheep, count wolves
#> 
#> Turtle metrics (output)
#>      = 
#> 
#> Patch metrics (output)
#>     NA
#> 
#> Link metrics (output)
#>      = 
#> 
#> Variable parameters (input)
#>     initial-number-sheep = list(min = 50, max = 150, step = 10, qfun = "qunif")
#>     initial-number-wolves = list(min = 50, max = 150, step = 10, qfun = "qunif")
#> 
#> Constant parameters (input)
#>     model-version = sheep-wolves-grass
#>     grass-regrowth-time = 30
#>     sheep-gain-from-food = 4
#>     wolf-gain-from-food = 20
#>     sheep-reproduce = 4
#>     wolf-reproduce = 5
#>     show-energy? = FALSE
#> 
#>    SIMDESIGN   
#> Simulation method      = lhs
#> Simulation object      = 
#> Generated random seeds = -108303981
#> 
#> Parameter matrix (input)
#> # A tibble: 100 × 9
#>    `initial-number-sheep` `initial-number-wolves` `model-version`   
#>                     <dbl>                   <dbl> <chr>             
#>  1                  117.                    109.  sheep-wolves-grass
#>  2                   99.6                    56.1 sheep-wolves-grass
#>  3                   91.7                    82.3 sheep-wolves-grass
#>  4                  115.                     57.5 sheep-wolves-grass
#>  5                   84.6                   111.  sheep-wolves-grass
#>  6                  120.                    125.  sheep-wolves-grass
#>  7                   54.6                   139.  sheep-wolves-grass
#>  8                   90.5                   147.  sheep-wolves-grass
#>  9                   50.3                    93.7 sheep-wolves-grass
#> 10                  111.                    119.  sheep-wolves-grass
#>    `grass-regrowth-time` `sheep-gain-from-food` `wolf-gain-from-food`
#>                    <dbl>                  <dbl>                 <dbl>
#>  1                    30                      4                    20
#>  2                    30                      4                    20
#>  3                    30                      4                    20
#>  4                    30                      4                    20
#>  5                    30                      4                    20
#>  6                    30                      4                    20
#>  7                    30                      4                    20
#>  8                    30                      4                    20
#>  9                    30                      4                    20
#> 10                    30                      4                    20
#>    `sheep-reproduce` `wolf-reproduce` `show-energy?`
#>                <dbl>            <dbl> <lgl>         
#>  1                 4                5 FALSE         
#>  2                 4                5 FALSE         
#>  3                 4                5 FALSE         
#>  4                 4                5 FALSE         
#>  5                 4                5 FALSE         
#>  6                 4                5 FALSE         
#>  7                 4                5 FALSE         
#>  8                 4                5 FALSE         
#>  9                 4                5 FALSE         
#> 10                 4                5 FALSE         
#> # ℹ 90 more rows
#> 
#> Simulation results (output)
#> # A tibble: 100 × 15
#>    `[run number]` `model-version`    `grass-regrowth-time`
#>             <int> <chr>                              <dbl>
#>  1              1 sheep-wolves-grass                    30
#>  2              2 sheep-wolves-grass                    30
#>  3              3 sheep-wolves-grass                    30
#>  4              4 sheep-wolves-grass                    30
#>  5              5 sheep-wolves-grass                    30
#>  6              6 sheep-wolves-grass                    30
#>  7              7 sheep-wolves-grass                    30
#>  8              8 sheep-wolves-grass                    30
#>  9              9 sheep-wolves-grass                    30
#> 10             10 sheep-wolves-grass                    30
#>    `sheep-gain-from-food` `wolf-gain-from-food` `sheep-reproduce`
#>                     <dbl>                 <dbl>             <dbl>
#>  1                      4                    20                 4
#>  2                      4                    20                 4
#>  3                      4                    20                 4
#>  4                      4                    20                 4
#>  5                      4                    20                 4
#>  6                      4                    20                 4
#>  7                      4                    20                 4
#>  8                      4                    20                 4
#>  9                      4                    20                 4
#> 10                      4                    20                 4
#>    `wolf-reproduce` `show-energy?` `initial-number-sheep`
#>               <dbl> <lgl>                           <dbl>
#>  1                5 FALSE                           117. 
#>  2                5 FALSE                            99.6
#>  3                5 FALSE                            91.7
#>  4                5 FALSE                           115. 
#>  5                5 FALSE                            84.6
#>  6                5 FALSE                           120. 
#>  7                5 FALSE                            54.6
#>  8                5 FALSE                            90.5
#>  9                5 FALSE                            50.3
#> 10                5 FALSE                           111. 
#>    `initial-number-wolves` `random-seed` `[step]` `count sheep` `count wolves`
#>                      <dbl>         <dbl>    <dbl>         <dbl>          <dbl>
#>  1                   109.     -108303981       10            92            109
#>  2                    56.1    -108303981       10            90             69
#>  3                    82.3    -108303981       10            76             92
#>  4                    57.5    -108303981       10           128             69
#>  5                   111.     -108303981       10            62            112
#>  6                   125.     -108303981       10            84            145
#>  7                   139.     -108303981       10            47            151
#>  8                   147.     -108303981       10            53            170
#>  9                    93.7    -108303981       10            35            108
#> 10                   119.     -108303981       10            91            131
#>    siminputrow
#>          <int>
#>  1           1
#>  2           2
#>  3           3
#>  4           4
#>  5           5
#>  6           6
#>  7           7
#>  8           8
#>  9           9
#> 10          10
#> # ℹ 90 more rows
#> 
#>    SUMMARY   
#> supported nlversion: ✓
#> NetLogo installation exists on local system: ✗
#> modelpath exists on local system: ✗
#> valid jvm memory: ✓
#> valid experiment name: ✓
#> outpath exists on local system: ✗
#> setup and go defined: ✓
#> variables defined: ✓
#> constants defined: ✓
#> metrics defined: ✓
#> spatial Metrics defined: ✓
#> simdesign attached: ✓
#> siminput parameter matrix: ✓
#> number of siminputrows: 100
#> number of random seeds: 1
#> estimated number of runs: 100
#> simoutput results attached: ✓
#> number of runs calculated: 100
```

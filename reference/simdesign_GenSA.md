# Add a Simulated Annealing simdesign to a nl object

Add a Simulated Annealing simdesign to a nl object

## Usage

``` r
simdesign_GenSA(nl, par = NULL, evalcrit = 1, control = list(), nseeds = 1)
```

## Arguments

- nl:

  nl object with a defined experiment

- par:

  optional vector of start values, one for each variable of the
  experiment, in the order in which the variables are defined. If NULL
  (default), GenSA draws a random start point within the parameter
  boundaries.

- evalcrit:

  position of evaluation criterion within defined NetLogo metrics of nl
  experiment or a function that reports a single numeric value

- control:

  list with further arguments passed to the GenSA function (see ?GenSA
  for details)

- nseeds:

  number of seeds for this simulation design

## Value

simdesign S4 class object

## Details

This function creates a simdesign S4 class which can be added to a nl
object.

Every evaluation of the optimization is one NetLogo run (or
`nreplicates` runs, see
[run_nl_dyn](https://docs.ropensci.org/nlrx/reference/run_nl_dyn.md)),
which takes from seconds to minutes depending on the model.
[run_nl_dyn](https://docs.ropensci.org/nlrx/reference/run_nl_dyn.md)
reports the number of evaluations when it starts and shows their
progress. With an empty `control` list, GenSA runs with its defaults
(`maxit = 5000`), which amounts to tens of thousands of evaluations; set
a stop criterion such as `max.call` or `max.time` in `control`.

Variables in the experiment variable list need to provide a numeric
distribution with min and max (e.g. list(min=1, max=4)). Only min and
max are used: the algorithm searches the range they define, so a qfun of
the variable definition is irrelevant for this simdesign.

The GenSA simdesign generates a simulated Annealing experiment within
the defined min and max parameter boundaries that are defined in the
variables field of the experiment object within the nl object.

The evalcrit reporter defines the evaluation criterion for the simulated
annealing procedure. There are two options to evaluate the fitness value
of each iteration of the algorithm:

1.  Use a reporter that is defined within the experiment metrics vector.
    You can just enter the position of that metric within the experiment
    metrics vector (e.g. 1 would use the first defined metric of the
    experiment to evaluate each iteration). The algorithm automatically
    calculates the mean value of this reporter if evalticks is defined
    to measure multiple ticks during each simulation. You can define a
    function that post-processes NetLogo output to calculate an
    evaluation value. This function must accept the nl object as input
    and return one single numeric value. The nl object that is then
    provided to the evaluation function will have results of the current
    iteration attached. The results can be accessed via the simoutput
    slot of the simdesign. You can pass this function to evalcrit. It is
    then applied to the output of each iteration.

The function uses the GenSA package to set up a Simulated Annealing
function. For details on the GenSA function parameters see ?GenSA
Finally, the function reports a simdesign object.

Simulated Annealing simdesigns can only be executed using the
[run_nl_dyn](https://docs.ropensci.org/nlrx/reference/run_nl_dyn.md)
function instead of
[run_nl_all](https://docs.ropensci.org/nlrx/reference/run_nl_all.md) or
[run_nl_one](https://docs.ropensci.org/nlrx/reference/run_nl_one.md).

## Examples

``` r

# To attach a simdesign, a nl object needs to be created first (see ?nl).
# For this example, we load a nl object from test data.

nl <- nl_lhs

# Example 1: Using a metric from the experiment metrics vector for evaluation:
nl@simdesign <- simdesign_GenSA(nl=nl,
                                 par=NULL,
                                 evalcrit=1,
                                 control=list(max.time = 600),
                                 nseeds=1)
#> Creating GenSA simulation design


# Example 2: Using a self-defined evaluation function
# For demonstration we define a simple function that calculates
# the maximum value of count sheep output.
critfun <- function(nl) {
results <- nl@simdesign@simoutput
crit <- as.integer(max(results$`count sheep`))
return(crit)
}

nl@simdesign <- simdesign_GenSA(nl=nl,
                                 par=NULL,
                                 evalcrit=critfun,
                                 control=list(max.time = 600),
                                 nseeds=1)
#> Creating GenSA simulation design

```

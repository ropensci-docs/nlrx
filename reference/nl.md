# Construct a new nl object

Construct a new nl object

## Usage

``` r
nl(
  nlversion = "7.0.4",
  nlpath = Sys.getenv("NETLOGO_HOME"),
  modelpath = character(),
  jvmmem = 1024,
  experiment = methods::new("experiment"),
  simdesign = methods::new("simdesign"),
  check_version = TRUE,
  ...
)
```

## Arguments

- nlversion:

  A character string defining the NetLogo version that is used

- nlpath:

  Path to the NetLogo main directory matching the defined version.
  Defaults to the `NETLOGO_HOME` environment variable, so it can be
  omitted when that is set. When a path is given, it takes precedence:
  it is used for the duration of each
  [`run_nl_all`](https://docs.ropensci.org/nlrx/reference/run_nl_all.md)
  /
  [`run_nl_one`](https://docs.ropensci.org/nlrx/reference/run_nl_one.md)
  /
  [`run_nl_dyn`](https://docs.ropensci.org/nlrx/reference/run_nl_dyn.md)
  call, so one nl object can be run against a different NetLogo
  installation than another without changing the session

- modelpath:

  Path to the NetLogo model file (.nlogox) that is used for simulations.
  NetLogo 6 model files (.nlogo) are rejected; open them in NetLogo 7
  and save them to convert them. Since NetLogo 6.3.0 the models shipped
  with NetLogo are stored at the installation root, so a sample model is
  reached with `file.path(nlpath, "models/Sample Models/...")`

- jvmmem:

  Java virtual machine memory capacity in megabytes

- experiment:

  Holds a experiment S4 class object

- simdesign:

  Holds a simdesign S4 class object

- check_version:

  Logical. If TRUE (default), the NetLogo version is checked against the
  versions nlrx is tested with
  ([supported_netlogo_versions](https://docs.ropensci.org/nlrx/reference/supported_netlogo_versions.md)):
  an untested NetLogo 7.x version emits a warning and is accepted, a
  version below 7.0.0 is an error. Set to FALSE to silence the warning.

- ...:

  ...

## Value

nl S4 class object

## Details

nl objects are the main class objects used in the nlrx package. These
objects store all information that is needed to run NetLogo simulations.
nl objects are initialized with basic information on Netlogo and the
model.

After setting up the nl object, an experiment needs to be attached. The
experiment class stores all information related to the NetLogo
simulation experiment, such as runtime, variables, constants,
measurements, and more.

After attaching an experiment, different simdesign helper functions can
be used to attach a simdesign to the nl object. The simdesign helper
functions use the variable definitions from the experiment within the nl
object to generate a parameter tibble for simulations.

## Examples

``` r
# Example for Wolf Sheep Predation model from NetLogo models library:
# Windows default NetLogo installation path (adjust to your needs!):
netlogopath <- file.path("C:/Program Files/NetLogo 7.0.4")
modelpath <- file.path(netlogopath, "models/Sample Models/Biology/Wolf Sheep Predation.nlogox")
outpath <- file.path("C:/out")
# Unix default NetLogo installation path (adjust to your needs!):
netlogopath <- file.path("/home/NetLogo 7.0.4")
modelpath <- file.path(netlogopath, "models/Sample Models/Biology/Wolf Sheep Predation.nlogox")
outpath <- file.path("/home/out")

nl <- nl(nlversion = "7.0.4",
         nlpath = netlogopath,
         modelpath = modelpath,
         jvmmem = 1024)
```

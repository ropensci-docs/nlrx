# Changelog

## nlrx (development version)

## nlrx 0.5.0

CRAN release: 2026-11-25

nlrx now runs NetLogo 7 and newer through the ‘logolink’ package, and
support for NetLogo 6 and older has been removed. NetLogo 6 models
(`.nlogo`) have to be converted once in NetLogo 7, see the NetLogo
transition guide: <https://docs.netlogo.org/transition>. To keep working
with NetLogo 6, install nlrx 0.4.6:
`remotes::install_github("ropensci/nlrx@v0.4.6")`.

### Breaking changes

- Support for NetLogo versions prior to 7.0.0 has been removed. NetLogo
  (\>= 7.0.0) and ‘logolink’ (\>= 1.0.0) are now required to run
  simulations. The legacy execution backend (OS-specific batch-file
  generation and direct NetLogo calls) has been removed; execution is
  delegated entirely to ‘logolink’.
- NetLogo 7 introduced a new model file format (`.nlogox`) and converts
  widget sizes. Models created in older NetLogo versions must be opened
  and re-saved in NetLogo 7 before they can be used with nlrx. See the
  NetLogo transition guide for details:
  <https://docs.netlogo.org/transition>.
  [`nl()`](https://docs.ropensci.org/nlrx/reference/nl.md),
  [`report_model_parameters()`](https://docs.ropensci.org/nlrx/reference/report_model_parameters.md),
  [`nldoc()`](https://docs.ropensci.org/nlrx/reference/nldoc.md) and the
  run functions stop with this advice when they are given a `.nlogo`
  file. NetLogo 7 would convert such a file on the fly, but nlrx cannot
  read the old format to check parameters.
- [`run_nl_all()`](https://docs.ropensci.org/nlrx/reference/run_nl_all.md)
  no longer parallelises through the ‘future’ package: a
  `future::plan()` has no effect anymore. Simulations are bundled into
  blocks that run in one NetLogo instance each, parallelised with
  NetLogo’s native multithreading (`threads`, see New features). To
  distribute simulations over several machines, split the simdesign into
  chunks, as shown for ‘rslurm’ in the “Advanced configuration” article:
  <https://docs.ropensci.org/nlrx/articles/furthernotes.html>.
- The `repetition` slot of the experiment class has been removed,
  together with the `repetition` argument of
  [`experiment()`](https://docs.ropensci.org/nlrx/reference/experiment.md).
  Repetitions were executed by NetLogo BehaviorSpace with seeds that
  nlrx neither controlled nor reported, so repeated runs could not be
  reproduced, and with more than one repetition the results could not be
  mapped back to their parameterisation reliably. Passing
  `repetition = 1` still works but emits a deprecation warning and has
  no effect; `repetition > 1` is an error. Use `nseeds` in the simdesign
  helpers instead, or `nreplicates` in
  [`run_nl_dyn()`](https://docs.ropensci.org/nlrx/reference/run_nl_dyn.md)
  for dynamic designs.
- The `seed` argument of
  [`run_nl_dyn()`](https://docs.ropensci.org/nlrx/reference/run_nl_dyn.md)
  is deprecated. The seeds of the simdesign are used instead, as in
  [`run_nl_all()`](https://docs.ropensci.org/nlrx/reference/run_nl_all.md).
  Passing `seed` still works for this release but emits a deprecation
  warning; to run a subset of the seeds, reduce them with
  `setsim(nl, "simseeds") <- ...`. Note that the return value of
  [`run_nl_dyn()`](https://docs.ropensci.org/nlrx/reference/run_nl_dyn.md)
  changed with this (see New features).
- NetLogo literals can no longer be used as parameter values. Since
  ‘logolink’ quotes every character value and offers no escape hatch, a
  value such as `"[1 2 3]"` reaches NetLogo as a string instead of a
  list.
  [`eval_variables_constants()`](https://docs.ropensci.org/nlrx/reference/eval_variables_constants.md)
  reports values that look like list literals; define such globals
  within the model instead.
- The arguments `split`, `cleanup.csv`, `cleanup.xml`, `cleanup.bat` and
  `writeRDS` are deprecated and no longer have an effect (file handling
  is managed by ‘logolink’). Passing them now emits a deprecation
  warning.
- The `n_cluster` argument of the ABC-MCMC simdesigns
  ([`simdesign_ABCmcmc_Marjoram()`](https://docs.ropensci.org/nlrx/reference/simdesign_ABCmcmc_Marjoram.md),
  [`simdesign_ABCmcmc_Marjoram_original()`](https://docs.ropensci.org/nlrx/reference/simdesign_ABCmcmc_Marjoram_original.md),
  [`simdesign_ABCmcmc_Wegmann()`](https://docs.ropensci.org/nlrx/reference/simdesign_ABCmcmc_Wegmann.md))
  has been removed. It never parallelised simulations (it was always
  reset to 1) and is now deprecated; passing it emits a deprecation
  warning.

### New features

- Added support for NetLogo 7 and newer
  ([\#106](https://github.com/ropensci/nlrx/issues/106)). The simulation
  backend was redesigned around the ‘logolink’ package, which generates
  the BehaviorSpace XML and executes NetLogo.
- Simulations are now executed in blocks
  ([\#60](https://github.com/ropensci/nlrx/issues/60)).
  [`run_nl_all()`](https://docs.ropensci.org/nlrx/reference/run_nl_all.md)
  gains `block_size` (number of simulations bundled into one NetLogo
  instance) and `threads` (NetLogo’s native multithreading) arguments.
  Bundling many simulations as BehaviorSpace sub-experiments within a
  single NetLogo instance avoids the repeated JVM/NetLogo start-up of
  the previous one-process-per-run approach, which can substantially
  speed up larger designs
  ([\#94](https://github.com/ropensci/nlrx/issues/94),
  [\#95](https://github.com/ropensci/nlrx/issues/95),
  [\#101](https://github.com/ropensci/nlrx/issues/101)).
- [`run_nl_one()`](https://docs.ropensci.org/nlrx/reference/run_nl_one.md)
  now accepts a vector of random seeds and executes the parameterisation
  once per seed. The replicated runs are executed within one NetLogo
  instance and can be parallelised with `threads`.
- [`run_nl_dyn()`](https://docs.ropensci.org/nlrx/reference/run_nl_dyn.md)
  now runs one complete optimization for each random seed of the
  simdesign, instead of a single one for a seed given as an argument
  ([\#88](https://github.com/ropensci/nlrx/issues/88)). The results are
  returned as a tibble with one row per seed, holding the seed and the
  result object of the respective optimization in a `result` list
  column. The objects are stored as the optimization packages return
  them, so their summary and plot functions still apply
  (`results$result[[1]]`). A failing optimization no longer discards the
  results of the other seeds: its error is stored in the `result` column
  and a warning names the affected seeds.
- [`run_nl_dyn()`](https://docs.ropensci.org/nlrx/reference/run_nl_dyn.md)
  gains an `nreplicates` argument. Each parameterisation proposed by a
  dynamic simdesign (`GenSA`, `GenAlg`, `ABCmcmc_*`) is then simulated
  `nreplicates` times with different random seeds, which reduces the
  simulation noise of the evaluation criterion. The replicate seeds are
  derived from the simdesign seed of the optimization and are identical
  across its evaluations (common random numbers), so they do not have to
  be stored. The results are aggregated in two steps, first over the
  measured ticks of each run and then over the replicated runs, so that
  runs with more measured ticks do not weigh more.
- [`nldoc()`](https://docs.ropensci.org/nlrx/reference/nldoc.md)
  documents NetLogo 7 models (`.nlogox`). The GUI elements are read with
  the same parser as
  [`report_model_parameters()`](https://docs.ropensci.org/nlrx/reference/report_model_parameters.md),
  and the BehaviorSpace section covers the NetLogo 7 experiment
  definitions, including pre- and post-experiment commands, the
  measurement condition and sub-experiments. The `toc` and
  `number_sections` options now also apply to PDF output, and rendering
  no longer prints the pandoc command line.
- `nlpath` is optional. It defaults to the `NETLOGO_HOME` environment
  variable, so it can be omitted when that is set, and a given path
  takes precedence: `NETLOGO_HOME` is set to it for the duration of a
  run and restored afterwards, so different nl objects can use different
  NetLogo installations within one session. A missing installation is
  reported with a clear error, and an `nlpath` that does not exist on
  the current system (for example in an nl object restored with
  [`import_nl()`](https://docs.ropensci.org/nlrx/reference/import_nl.md))
  warns and falls back to `NETLOGO_HOME`.
- [`simdesign_morris()`](https://docs.ropensci.org/nlrx/reference/simdesign_morris.md)
  gains a `scale` argument. The input factors were always scaled to
  \[0,1\] before the elementary effects were computed; passing
  `scale = FALSE` now yields unscaled effects.

### Minor improvements

- [`run_nl_dyn()`](https://docs.ropensci.org/nlrx/reference/run_nl_dyn.md)
  tells upfront how many evaluations the optimization of each seed may
  take and shows their progress. Every evaluation is one NetLogo run, so
  the defaults of the dynamic simdesigns can take hours to days (for
  example 20,000 runs per seed for
  [`simdesign_GenAlg()`](https://docs.ropensci.org/nlrx/reference/simdesign_GenAlg.md)),
  which looked like a hanging session: each run printed its log lines
  without any indication of the total. The log lines of the single runs
  are now held back and only shown when a run fails, a progress bar
  counts the evaluations, and a GenSA simdesign without any stop
  criterion in `control` produces a warning. The defaults are unchanged;
  the examples and vignettes use settings that finish within minutes.
- Untested NetLogo 7 versions are no longer rejected.
  [`nl()`](https://docs.ropensci.org/nlrx/reference/nl.md) and
  [`download_netlogo()`](https://docs.ropensci.org/nlrx/reference/download_netlogo.md)
  now emit a warning and continue when the NetLogo version is not among
  the versions nlrx was tested with
  ([`supported_netlogo_versions()`](https://docs.ropensci.org/nlrx/reference/supported_netlogo_versions.md)):
  simulations are executed by ‘logolink’, so newer releases are likely
  to work without an nlrx update. Versions below 7.0.0 remain an error,
  since their backend was removed, and `check_version = FALSE` silences
  the warning.
- [`simdesign_ABCmcmc_Marjoram()`](https://docs.ropensci.org/nlrx/reference/simdesign_ABCmcmc_Marjoram.md)
  and
  [`simdesign_ABCmcmc_Wegmann()`](https://docs.ropensci.org/nlrx/reference/simdesign_ABCmcmc_Wegmann.md)
  check that the calibration keeps at least two runs
  (`ceiling(tolerance_quantile * n_calibration) >= 2`). With fewer,
  ‘EasyABC’ failed with an obscure “subscript out of bounds” or
  “incorrect number of dimensions” error after the whole calibration had
  run.
- Errors and warnings about the setup (NetLogo version, model format,
  export path, dynamic simdesign settings) explain what is wrong and
  what to do, without a call or backtrace.
- String and boolean parameter values are expected as plain character
  values and logicals. ‘logolink’ quotes character values itself, so one
  layer of enclosing double quotes is removed from the values of
  constants and variables, and the escaped-quote convention of earlier
  nlrx versions (`"model-version" = "\"sheep-wolves-grass\""`) keeps
  working. Boolean strings (`"false"`, `"TRUE"`) are converted to
  logicals, for constants as well as variables.
- nlrx no longer depends on the ‘XML’ package; NetLogo model files are
  read with ‘xml2’.
- The sample data sets (`nl_lhs`, `nl_sobol`, …) were regenerated with
  NetLogo 7.0.4.

### Bug fixes

- `evalticks` are checked before and after the simulations
  ([\#111](https://github.com/ropensci/nlrx/issues/111)).
  [`experiment()`](https://docs.ropensci.org/nlrx/reference/experiment.md)
  reports ticks beyond the `runtime`, which are never measured, and,
  with `tickmetrics = "false"`, `evalticks` other than the `runtime`,
  which are ignored since metrics are then only measured on the last
  tick. After the simulations, requested ticks that carry no results are
  reported: simulations can end before a requested tick is reached,
  through `runtime` or a `stopcond`, in which case the results silently
  contained fewer ticks than asked for. nlrx 0.4.x intended such a
  message, but its index expression
  (`evalticks[!which(evalticks %in% steps)]`) coerced indices to logical
  and could never select anything.
- `simdesign_GenSA(par = )` is no longer ignored. The start values were
  stored in the simdesign, but
  [`GenSA::GenSA()`](https://rdrr.io/pkg/GenSA/man/GenSA.html) was
  always called with `par = NULL`, so every optimization started from a
  random point within the parameter boundaries. The values are now
  passed through, and
  [`simdesign_GenSA()`](https://docs.ropensci.org/nlrx/reference/simdesign_GenSA.md)
  checks them against the number, order and boundaries of the experiment
  variables.
- Models that use NetLogo extensions no longer fail with “Can’t find
  extension” ([\#77](https://github.com/ropensci/nlrx/issues/77),
  [\#98](https://github.com/ropensci/nlrx/issues/98)). Extensions are
  resolved by NetLogo itself again, instead of depending on the
  directories and Java options that the former backend prepared.
- Simulation results are no longer lost when the execution blocks report
  a metric with different types
  ([\#110](https://github.com/ropensci/nlrx/issues/110),
  [\#90](https://github.com/ropensci/nlrx/issues/90)). A run whose
  metric returns a NetLogo error message made the binding of the blocks
  fail, which discarded the results of every completed run. Such columns
  are converted to character instead, with a warning naming them.
- [`download_netlogo()`](https://docs.ropensci.org/nlrx/reference/download_netlogo.md)
  fetches the macOS disk image that matches the architecture of the
  machine. It always requested the Intel (`x86_64`) image, so users on
  Apple Silicon received a build for the wrong architecture. The
  architecture is now detected, also under Rosetta, and can be set
  explicitly with the new `arch` argument.
- [`download_netlogo()`](https://docs.ropensci.org/nlrx/reference/download_netlogo.md)
  is more robust. A version that does not exist now stops with a pointer
  to the NetLogo releases page instead of the raw “HTTP status was ‘404
  Not Found’” error, and other failed downloads are reported as such; a
  partially downloaded file is removed. The download timeout is raised
  to at least one hour, because R’s default of 60 seconds is often too
  short for the NetLogo archives of about 400 MB. The installer is
  downloaded as a binary file, which a text transfer corrupted on
  Windows (`.msi`). The archive is extracted with
  [`utils::untar()`](https://rdrr.io/r/utils/untar.html), which works
  with paths that contain spaces and no longer lists every file. The
  function returns the path of the downloaded file.
- [`export_nl()`](https://docs.ropensci.org/nlrx/reference/export_nl.md)
  no longer archives more than the exported folder. A relative `path`
  such as `"."` made it pack the whole working directory and then the
  whole R session’s temporary directory, and folders of earlier exports
  in the same session were mixed into the archive. The archive is now
  assembled in a staging folder of its own and written with
  [`utils::tar()`](https://rdrr.io/r/utils/tar.html), without listing
  every file in the console. The home directory and the filesystem root
  are refused, as is an archive stored within the exported folder, and a
  message reports how many files were exported.
  [`export_nl()`](https://docs.ropensci.org/nlrx/reference/export_nl.md)
  returns the path of the archive invisibly.
- [`import_nl()`](https://docs.ropensci.org/nlrx/reference/import_nl.md)
  returns the imported nl object (invisibly) instead of the status of
  the `tar` command, and `new_session = TRUE` opens the `.Rproj` file of
  the extracted folder. It looked for that file within the archive file
  itself, so it never found one. Archives that hold no `nlobject.rds`
  are rejected before anything is extracted.
- [`nldoc()`](https://docs.ropensci.org/nlrx/reference/nldoc.md) no
  longer fails on models without complete noxygen annotations. A model
  without an `@model` header failed with “missing value where TRUE/FALSE
  needed”, and one without `@global` or `@procedure` tags with “argument
  is of length zero”. Without a header, the name of the model file is
  now used as title; sections without documented globals or procedures
  are left out, and a message points out when the model has no
  annotations at all.

## nlrx 0.4.6

CRAN release: 2025-11-25

### Functionality

- Updated readr::file_write function to avoid pkg break due to
  deprecation
- added support to download_netLogo() for up to NetLogo version 6.4.0

## nlrx 0.4.5

CRAN release: 2024-01-29

### Functionality

- No functionality updates

### Bugfixes

- documentation update to fix CRAN check notes

## nlrx 0.4.4

CRAN release: 2023-05-16

### Functionality

- added support to download_netLogo() for up to NetLogo version 6.3.0
- adjusted test_nlrx() to work with new NetLogo directory structure
  (6.3.0)
- added writeRDS parameter to run_nl_all() for storing intermediate
  results

### Bugfixes

- updating Java Version Requirement in DESCRIPTION
- refactoring download_netlogo function
- Fix readr problems with util_runnl() (deprecated in path argument in
  write_lines)
- Fix path problems
- Fix to allow for list output in agent variables (metrics.turtles,
  metrics.patches, metrics.links)

## nlrx 0.4.3

CRAN release: 2021-09-20

### Functionality

- added test_nlrx() function to check functionality of the package
- added support to download_netLogo() for NetLogo version 6.2.0

### Bugfixes

- changed timestamp for nldoc function from lubridate to base date
- fixed an error in the function parser of the nldoc procedure
- fixed bug in calculation of number of computed runs in print_nl()

## nlrx 0.4.2

CRAN release: 2020-11-13

### Functionality

- added option to run_nl_one that allows to store results as rds files
- added eval_simoutput option to check for missing combinations of
  siminputrow and random-seeds
- added support for progressr progress bars for run_nl_all function
  (details see further notes vignette) and removed the silent parameter
  of the run_nl_all function

### Bugfixes

- hotfix for another dependency on external files in nldoc roxygen
  examples
- small bugfix in analyze_morris: A warning is now thrown if NA are
  present in the simulation data
- bugfix in random seed generator
- bugfix for sobol simulation design when sobolorder is higher than the
  available number of variables
- analyze_nl now prints a warning if missing combinations were detected
  in the simulation output
- updated testdata
- user rights for temporary sh scripts are now set correctly

## nlrx 0.4.1

CRAN release: 2020-02-07

- fixed dependency on external file source in nldoc automated tests
- these files are now included in the package
- added link to documentation website in description

## nlrx 0.4.0

CRAN release: 2019-12-03

- Added new simdesigns simdesign_ABCmcmc_Marjoram,
  simdesign_ABCmcmc_Marjoram_original and simdesign_ABCmcmc_Wegmann to
  perform approximate bayesian computation
- Added print function for nl objects
- Added dependencies: crayon, EasyABC
- Added pandoc to system requirements
- Added additional pandoc_available() check for nldoc function
- Added support to download_netLogo() for NetLogo version 6.1.1
- Added new vignette showing an example for approximate bayesian
  computation with nlrx
- Updated “Sensitivity Analyses with nlrx”” vignette
- Updated “Advanced Configuration” vignette
- Updated package tests

## nlrx 0.3.0

CRAN release: 2019-09-26

- Added support for self-defined evaluation functions to optimization
  functions simdesign_GenAlg and simdesign_GenSA.
- Added support to simdesign_simple() for models without any GUI
  parameters
- Added support to download_netLogo() for NetLogo version 6.1.0
- Added new vignette showing an example for Sensitivity Analysis with
  nlrx.
- Added new vignette showing an example for Optimization with nlrx.
- Updated “Advanced Configuration” vignette.
- Updated citation information of the package.
- Hotfix for unnest_simoutput(). In the previous package version, under
  some circumstances an error occured due to NA data.
- Corrected spelling errors in some vignettes and documentation files.

## nlrx 0.2.0

CRAN release: 2019-03-28

- nl_to_raster() hotfix

## nlrx 0.1.0

CRAN release: 2019-03-18

- First release to CRAN.

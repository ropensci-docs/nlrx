# Import NetLogo Experiment

Import NetLogo Experiment from export_nl

## Usage

``` r
import_nl(tarfile, targetdir, new_session = FALSE)
```

## Arguments

- tarfile:

  Path to tarfile that contains files to run NetLogo experiment

- targetdir:

  Path to folder where the experiments gets extracted

- new_session:

  If TRUE, opens a new RStudio Session with an Rproj

## Value

The imported nl object, invisibly.

## Details

Imports NetLogo experiments that were saved with `export_nl`. The
archived folder is extracted into `targetdir` and the nl object stored
with it is returned. If the folder comes with an .Rproj file (which is
recommended because relative paths enhance the reproducability of your
analysis), `import_nl` can open this project in a new RStudio session
(`new_session = TRUE`).

Note that the paths stored in the nl object (`nlpath`, `modelpath`,
`outpath`) still point to the locations on the machine the experiment
was exported from.

## Examples

``` r
if (FALSE) { # \dontrun{

infile <- "/home/user/test.tar.gz"
targetdirectory <- "/home/user/test"
nl <- import_nl(infile, targetdirectory)
} # }
```

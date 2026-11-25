# Export NetLogo Experiment

Export NetLogo Experiment as tar.gz file

## Usage

``` r
export_nl(nl, path = dirname(getnl(nl, "modelpath")), tarfile)
```

## Arguments

- nl:

  nl object

- path:

  Path to folder that contains files to run NetLogo experiment

- tarfile:

  Path to the tar.gz file the experiment gets stored in

## Value

The path of the created tar.gz file, invisibly.

## Details

Exports your folder that contains data and scripts for NetLogo + nlrx
analyses as a tar.gz file. Furthermore, `export_nl` takes your nl object
and saves it as `nlobject.rds` in the archived folder. This enables
other person to run the same experiment as you. The folder itself is not
changed.

By default, the folder that contains the NetLogo model is exported.
Everything in that folder ends up in the archive, so keep the model in a
project folder of its own. The home directory and the filesystem root
are refused, and the tar.gz file must not be stored within the exported
folder.

## Examples

``` r
if (FALSE) { # \dontrun{

# Load nl object from testdata:
nl <- nl_lhs
path <- getwd() # adjust path to your needs, path should point to a directory with model data
outfile <- tempfile(fileext = ".tar.gz") # adjust file path to your needs
export_nl(nl, path = path, tarfile = outfile)
} # }
```

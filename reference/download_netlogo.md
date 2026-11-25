# Download NetLogo

Auxiliary function to download NetLogo

## Usage

``` r
download_netlogo(to, version, os = NA, extract = FALSE, arch = NA)
```

## Arguments

- to:

  Path to folder where the downloaded file is saved.

- version:

  Character string naming which NetLogo Version to download (see
  Details)

- os:

  operation system ("win", "mac", "unix") decides which version of
  netlogo (msi, dmg, tgz) is downloaded. If set to NA (default) os will
  be detected automatically
  ([`util_get_os()`](https://docs.ropensci.org/nlrx/reference/util_get_os.md))

- extract:

  TRUE/FALSE, if TRUE downloaded archive is extracted to subfolder of
  `to` (only unix)

- arch:

  macOS architecture of the disk image, "aarch64" (Apple Silicon) or
  "x86_64" (Intel). If NA (default) the architecture of the running
  machine is detected
  ([`util_get_mac_arch()`](https://docs.ropensci.org/nlrx/reference/util_get_mac_arch.md)).
  Ignored for Windows and Linux, which have one download each.

## Value

The path of the downloaded file, invisibly.

## Details

Retrieve the versions nlrx is tested with (parameter `version`):
supported_netlogo_versions()

Newer NetLogo 7 releases can be downloaded as well: the download URL is
derived from the version number, so an untested version only emits a
warning
([check_netlogo_version](https://docs.ropensci.org/nlrx/reference/check_netlogo_version.md))
and fails with an error pointing to the NetLogo releases page if no such
release exists.

The download (about 400 MB) may take longer than R's default `timeout`
of 60 seconds, so the timeout is raised to at least one hour while it
runs.

## Examples

``` r
if (FALSE) { # \dontrun{
dlpath <- tempdir()  # adjust path to your needs
try(download_netlogo(dlpath, "7.0.4"))
} # }
```

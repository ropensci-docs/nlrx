# Report the macOS architecture

Reports which macOS architecture a NetLogo disk image should be
downloaded for

## Usage

``` r
util_get_mac_arch()
```

## Value

"aarch64" on Apple Silicon, "x86_64" otherwise

## Details

Under Rosetta, R reports `x86_64` even on Apple Silicon, so the hardware
is asked directly via `sysctl hw.optional.arm64` in that case. Pass
`arch` to
[download_netlogo](https://docs.ropensci.org/nlrx/reference/download_netlogo.md)
to override the result, for example to fetch an image for a different
machine.

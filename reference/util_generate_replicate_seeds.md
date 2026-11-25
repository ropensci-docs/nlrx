# Derive a vector of replicate seeds from a single design seed

Derive a reproducible vector of random seeds for replicated model runs

## Usage

``` r
util_generate_replicate_seeds(seed, nreplicates)
```

## Arguments

- seed:

  the design seed the replicate seeds are derived from

- nreplicates:

  number of replicate seeds to derive

## Value

numeric vector of length `nreplicates`

## Details

The derived seeds are a deterministic function of `seed` and therefore
do not need to be stored: the same `seed` always yields the same
replicate seeds. Because the seeds are drawn from the head of one
stream, the seed vector for a smaller `nreplicates` is a prefix of the
vector for a larger one.

The random number generator state of the calling environment is saved
and restored, so that deriving replicate seeds does not interfere with
the random number stream of the dynamic simulation designs (`genalg` and
`EasyABC` draw from it).

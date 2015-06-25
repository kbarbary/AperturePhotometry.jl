# AperturePhotometry

Aperture photometry functions for Julia

In astronomy, aperture photometry is summing an image's pixel values
within some region. It is often used to measure the brightness of
objects (such as stars or galaxies) that extend over many
pixels. While this is basically a simple sum operation, it is often
desireable to account for noise (possibly stored in a separate array)
and masked (bad) pixels. It is also desireable to account for precise
overlap between the region and pixel boundaries in order to reduce
sampling noise in the aperture.

```julia
flux = sum_circle(data, 5.0, 5.0, 3.0)
```
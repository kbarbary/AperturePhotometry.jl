AperturePhotometry.jl
=====================

Aperture photometry functions for Julia

In astronomy, aperture photometry is summing an image's pixel values
within some region. It is often used to measure the brightness of
objects (such as stars or galaxies) that extend over many
pixels. While this is basically a simple sum operation, it is often
desireable to account for noise (possibly stored in a separate array)
and masked ("bad") pixels. It is also desirable to account for precise
overlap between the region and pixel boundaries in order to reduce
sampling noise in the aperture.

Example:

```julia
flux, fluxerr = sum_circle(data, 5.0, 5.0, 3.0)
```

API
---

```julia
sum_circle(data, x, y, r; error=nothing, mask=nothing,
                          maskthresh=false, gain=1.0)
```

Sum within a circle centered at `x`, `y` with radius `r`.

```julia
sum_circann(data, x, y, rin, rout; error=nothing, mask=nothing,
                                   maskthresh=false, gain=1.0)
```

Sum within the circular annulus with inner radius `rin` and outer radius `rout`.

```julia
sum_ellipse(data, x, y, a, b, theta; error=nothing, mask=nothing,
                                     maskthresh=false, gain=1.0)
```

Sum within the ellipse with semi-major axis `a`, semi-minor axis `b` and
angle `theta` (angle of semi-major axis measured counter-clockwise from the
positive x axis).

----

In all cases, `data` is a 2-d array and the sum and error on the sum are
returned. The exact overlap between pixels and the aperture is calculated.
The error is calculated as `sqrt(sum(sigma_i^2) + flux/gain)`.
Optional arguments:

- `error`: standard deviation uncertainty on each pixel. Can be an array, a
  scalar (in which case the value applies to all pixels in the aperture), or
  `nothing`, which is equivalent to zero.

- `gain`: conversion factor between data array values and Poisson counts. See
  formula for error calculation above.

- `mask`: array giving masked pixels. Any element type is accepted pixels are
  considered masked if the value of the mask array is strictly greater than
  `maskthresh`.

License
-------

MIT

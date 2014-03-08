# Photometry

Astronomical photometry library for Julia

```julia
aper = CircAperture(10., 10., 5.)
flux, fluxerr = aperflux(aper, im)
```
:::{image} ./_static/logo_long.png
:align: center
:class: only-light
:::

:::{image} ./_static/logo_long_dark.png
:align: center
:class: only-dark
:::


# SurfATT Documentation

[![Language](https://img.shields.io/badge/-Fortran-734f96?logo=fortran&logoColor=white)](https://github.com/topics/fortran)

This is a package for **Surf**ace wave **A**djoint **T**ravel-time **T**omography .

SurfATT is a package for surface wave travel-time tomography, which is designed to invert surface wave travel-time data for 2D/3D isotropic or azimuthal anisotropic velocity structures with following features:

- Inversion for isotropic or azimuthal anisotropic media (Hao et al., 2024b, in preparation).
- Calculation of surface wave travel time based on Eikonal equation with fast sweeping method {cite:p}`tong2021a`.
- Computation of isotropic and anisotropic sensitivity kernels through adjoint method {cite:p}`tong2021b`.
- Multi-grid model parametrization utilization in optimization {cite:p}`tong2019`.
- Consideration of surface topography in forward and adjoint simulation {cite:p}`hao2023`.

:::{image} ./_static/framework.png
:align: center
:width: 500px
:class: only-light
:::

:::{image} ./_static/framework-dark.png
:align: center
:width: 500px
:class: only-dark
:::


SurfATT is an innovative package driven by modern Fortran with an embedded MPI parallel framework. It employs a user-friendly format for both input/output file types, including:

- `yaml` for input parameter files
- `csv` for input/output travel-time data files
- `hdf5` for input/output model files

Furthermore, this package provides optimal cross-platform compatibility; it operates perfectly on both personal computers and High-Performance Computing (HPC) systems.

```{toctree}
:caption: Installation
:maxdepth: 3
:hidden:

installation/dependence
installation/compile
```

```{toctree}
:caption: Usages
:titlesonly:
:maxdepth: 3
:hidden:

usages/src_rec
usages/rotate_src_rec
usages/topo
usages/tomography
```

```{toctree}
:caption: Development
:hidden:

contributor
GitHub <https://github.com/xumi1993/SurfATT-iso>
```

## References
:::{bibliography}
:style: unsrt
:::
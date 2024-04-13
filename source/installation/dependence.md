
# Dependencies

- git
- Fortran (Intel fortran or gfortran>11)
- C++
- hdf5 (serial version)
- CMake (v3.8 or higher)
- MPI (v3.0 or higher)


## Install dependencies on local computers

The compiler and some dependencies can be easily installed on personal computer via built-in software manager
::::{tab-set}

:::{tab-item} Conda
Opting to install SurfATT within a Conda environment is beneficial in scenarios where compiler or library conflicts arise due to dependencies of other software.
```
conda create -n surfatt -c conda-forge openmpi cxx-compiler fortran-compiler cmake hdf5
conda activate surfatt
```
If a compilation error related to the h5fortran library occurs, it may be due to an incompatibility with the hdf5 package installed via the conda-forge channel. In such cases, try to remove the hdf5 package from the Conda environment and utilize the hdf5 library integrated within h5fortran.
:::

:::{tab-item} Fedora
:sync: fedora

```
$ sudo dnf install gcc gcc-gfortran gcc-c++ cmake openmpi-devel hdf5-devel
```
:::

:::{tab-item} CentOS
:sync: CentOS

```
$ sudo dnf install gcc-toolset-11 cmake openmpi-devel hdf5-devel
```
:::

:::{tab-item} Ubuntu/Debian
:sync: ubuntu

```
$ sudo apt install build-essential gfortran cmake libopenmpi-dev openmpi-bin libhdf5-dev
```
:::

:::{tab-item} macOS
:sync: macos

```
$ brew install gcc cmake open-mpi hdf5
```
:::
::::

## Install dependencies on HPCs

The `module-environment` is extensively utilized for managing modules that are requisite for SurfATT. Dependencies can be loaded as illustrated below

::::{tab-set}
:::{tab-item} ASPIRE2A@NSCC
```
module purge && module load gcc/11.2.0-nscc libfabric/1.11.0.4.125 openmpi/4.1.5-gcc11 cmake/3.23.1 hdf5/1.10.5
```
:::
:::{tab-item} T6@BSCC
```
module purge && module load mpi/intel/20.0.4 hdf5/1.10.6-intel20 cmake/3.23.1 
```
:::
::::

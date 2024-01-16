
# Dependencies

- git
- Fortran (intel fortran or gfortran>11)
- hdf5 (serial version)
- C++
- CMake (3.8 or higher)
- MPI (v3.0 or higher)
- fypp (required by external lib [fortran-stdlib](https://github.com/fortran-lang/stdlib))


## Install dependencies on local computers
The compiler and some dependencies can be easily installed on personal computer via built-in software manager
::::{tab-set}

:::{tab-item} Fedora/CentOS
:sync: fedora

```
$ sudo dnf install gcc gcc-gfortran gcc-c++ cmake openmpi-devel hdf5-devel
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

:::{tab-item} Conda
Opting to install SurfATT within a Conada environment is beneficial in scenarios where compiler or library conflicts arise due to dependencies of other software.
```
conda create -n surfatt -c conda-forge gfortran openmpi hdf5 fypp
conda activate surfatt
```
:::
::::

## Install dependencies on HPCs

The `module-environment` is extensively utilized for managing modules that are requisite for SurfATT. Dependencies can be loaded as illustrated below

::::{tab-set}
:::{tab-item} ASPIRE2A@NSCC
```
module purge && module load gcc/11.2.0-nscc libfabric/1.11.0.4.125 openmpi/4.1.5-gcc11 cmake/3.23.1
```
:::
:::{tab-item} T6@BSCC
```
module load mpi/intel/20.0.4 hdf5/1.10.6-intel20 cmake/3.23.1 
```
:::
::::

## Install `fypp`

`fypp` is required by [fortran-stdlib](https://github.com/fortran-lang/stdlib), which can be easily installed via the `pip`:

```
pip install fypp
```

There are multiple method for installing `fypp`. Please see [fypp documentation](https://fypp.readthedocs.io/en/stable/fypp.html#installing) for detailed instructions.

# Download and compile SurfATT


## Clone the source codes

```
git clone --recursive https://github.com/xumi1993/SurfATT
```
`--recursive` is required in this command, because dependencies of `yaml-cpp`, `h5fortran`, and `fortran-stdlib` will be download automatically.

<!-- :::{admonition} For chinese users
:class: note

If the github is not accessible, please download source code from NJU gitlab
::: -->

## Install on local computers

The code can be compiled with cmake

```
mkdir build && cd build
cmake .. && make -j4
```

## Install on HPC

### Install `hdf5` for Fortran

In the case of HPCs where `hdf5` for Fortran might not be pre-installed, it is possible to manually compile and install `hdf5`.

``` bash
cd ./SurfATT/external_libs

# make a local install path
mkdir local_hdf5 

# download hdf5 source
wget https://support.hdfgroup.org/ftp/HDF5/releases/hdf5-1.13/hdf5-1.13.3/src/hdf5-1.13.3.tar.gz

# extract the downloaded directory
tar -xvf hdf5-1.13.3.tar.gz
cd hdf5-1.13.3/

# configure
CC=mpicc CXX=mpic++ FC=gfortran ./configure --enable-unsupported --enable-shared --enable-fortran --prefix=$(pwd)/../local_hdf5

# make
make -j && make install
```


### Compile source code

```bash
# configure
CC=gcc CXX=g++ FC=gfortran MPIFC=mpif90 HDF5_ROOT=$(pwd)/../external_libs/local_hdf5 cmake ..

# make
make -j
```

Then the executable `surfatt_tomo` and `surftomo_cb_fwd` are created in the `bin` directory.
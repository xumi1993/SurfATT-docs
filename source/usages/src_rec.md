# Preparation

The SurfATT package requires the travel-time data file and the input parameter file to perform the surface wave tomography inversion. The travel-time data file contains the observed surface wave travel-time, and the input parameter file contains the parameters for the inversion.

## Travel-time data file

The travel-time data can be obtained from the observed surface wave dispersion. The travel-time data should be stored in a `csv` file with the following columns:

- `tt`: travel time from the source to the receiver
- `staname`: station name
- `stla`: latitude of the station
- `stlo`: longitude of the station
- `stel`: elevation of the station in meters
- `evtname`: event name
- `evla`: latitude of the event
- `evlo`: longitude of the event
- `evel`: depth of the event in meters
- `period`: period of the surface wave
- `weight`: weight of the travel-time data
- `dist`: distance between the source and receiver (*optional*)
- `vel`: phase or group velocity of the surface wave (*optional*)

A template of the travel-time data file can be found [here](../_static/src_rec_file_ph.csv).

## Input parameter file

The input parameter file is in the `yaml` format. The input parameter file should contain the following sections with parameters:

### `data`

- `src_rec_file_ph`: path to the travel-time data file of phase velocity
- `src_rec_file_gr`: path to the travel-time data file of group velocity
- `iwave`: type of surface wave (1 Love wave (not included in the current version), 2 Rayleigh wave )
- `vel_type`: Bool list with 2 elements, indicating the type of velocity model e.g., `[True, False]` for phase velocity only.
- `weights`: Float list with 2 elements, indicating the weight of phase and group velocity data e.g., `[1.0, 0.0]` for phase velocity only.

### `domain`

- `depth`: List with 2 elements, indicating depth range of the model.
- `interval`: List with 3 elements, indicating the interval of the model along longitude, latitude, and depth.
- `num_grid_margin`: Int, indicating the grid number of margin area for the domain.
  
### `topo`

- `is_consider_topo`: Bool, indicating whether to consider the model with topography.
- `topo_file`: path to the surface topography file in `netcdf` format.
- `wavelen_factor`: Float, indicating the smoothing factor of the topography.

```{note}
We assume the `wavelen_factor` as {math}`\alpha` and the wavelength of the surface wave is {math}`\lambda`. A gaussian smoothing filter with a standard deviation of {math}`\sigma = \alpha \lambda` is applied to the topography.
```

### `output`

- `output_path`: path to the output files.
- `format`: output format of the model file (available for `hdf5` or `csv`).
- `log_level`: log level of the output (available for 0: `DEBUG`, 1:`INFO`).

### `inversion`

#### Initial model

- `init_model_type`: type of initial model (0: `1D`, 1: `3D`).
  - `0`: Increase from `vel_range[0]` to `vel_range[1]` linearly.
  - `1`: Do 1-D inversion first using the average surface wave velocity data.
  - `2`: Specify the 3-D initial model file with the same format as the output model file in hdf5 format.
- `vel_range`: List with 2 elements, indicating the range of the initial model.
- `init_model_path`: Path to the 3-D initial model file.

#### kernel Regularization

- `kdensity_coe`: Coefficient to rescale the final kernel:  kernel -> kernel / pow(density of kernel, Kdensity_coe).
- `ncomponents`: number of components of the inversion grids.
- `n_inv_grid`: Int list with 3 elements, indicating number of inversion grids along longitude, latitude, and depth.

#### Inversion parameters

- `niter`: maximum iteration number of the inversion.
- `min_derr`: minimum error change of the inversion.

#### Optimization parameters

- `optim_method`: Optimization method of the inversion (0: `Grad_descent`, 1: `Non-linear Conjugate Gradient`, 2: `L-BFGS`).
- `step_length`: Step length of the inversion.
- `max_sub_niter`: Maximum sub-iterations for line search.
- `maxshrink`: Maximum step length descent.
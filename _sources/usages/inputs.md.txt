# Input parameter file

The input parameter file is in the `yaml` format. The input parameter file should contain the following sections with parameters for the inversion:

## `data`

- `src_rec_file_ph`: path to the travel-time data file of phase velocity
- `src_rec_file_gr`: path to the travel-time data file of group velocity
- `iwave`: type of surface wave (1 Love wave (not included in the current version), 2 Rayleigh wave )
- `vel_type`: Bool list with 2 elements, indicating the type of velocity model e.g., `[True, False]` for phase velocity only.
- `weights`: Float list with 2 elements, indicating the weight of phase and group velocity data e.g., `[1.0, 0.0]` for phase velocity only.

## `domain`

- `depth`: List with 2 elements, indicating depth range of the model.
- `interval`: List with 3 elements, indicating the interval of the model along longitude, latitude, and depth.
- `num_grid_margin`: Int, indicating the grid number of margin area for the domain.
  
## `topo`

- `is_consider_topo`: Bool, indicating whether to consider the model with topography.
- `topo_file`: path to the surface topography file in `netcdf` format.
- `wavelen_factor`: Float, indicating the smoothing factor of the topography.

```{note}
We assume the `wavelen_factor` as {math}`\alpha` and the wavelength of the surface wave is {math}`\lambda`. A gaussian smoothing filter with a standard deviation of {math}`\sigma = \alpha \lambda` is applied to the topography.
```

## `output`

- `output_path`: path to the output files.
- `format`: output format of the model file (available for `hdf5` or `csv`).
- `log_level`: log level of the output (available for 0: `DEBUG`, 1:`INFO`).

## `inversion`

### Initial model

- `init_model_type`: type of initial model (0: `1D`, 1: `3D`).
  - `0`: Increase from `vel_range[0]` to `vel_range[1]` linearly.
  - `1`: Do 1-D inversion first using the average surface wave velocity data.
  - `2`: Specify the 3-D initial model file with the same format as the output model file in hdf5 format.
- `vel_range`: List with 2 elements, indicating the range of the initial model.
- `init_model_path`: Path to the 3-D initial model file.

### Kernel Regularization

- `kdensity_coe`: Coefficient to rescale the final kernel

```{note}
we assume the `kdensity_coe` as {math}`\alpha`. The kernel {math}`K` is rescaled as {math}`\frac{1}{K_{den}^\alpha}`, where the {math}`K_{den}` is the total kernel density. The `kdensity_coe` is usually set between 0.0 and 1.0.
```

- `ncomponents`: number of components of the inversion grids.
- `n_inv_grid`: Int list with 3 elements, indicating number of inversion grids along longitude, latitude, and depth.

### Inversion parameters

- `niter`: maximum iteration number of the inversion.
- `min_derr`: minimum error change of the inversion.

### Optimization parameters

- `optim_method`: Optimization method of the inversion (0: `Grad_descent`, 1: `Non-linear Conjugate Gradient`, 2: `L-BFGS`).

```{note}
The `L-BFGS` method is recommended, due to its fast convergence.
```

- `step_length`: Step length of the inversion.
- `max_sub_niter`: Maximum sub-iterations for line search.
- `maxshrink`: Maximum step length descent.
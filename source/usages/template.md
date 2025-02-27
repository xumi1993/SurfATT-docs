# Template of Parameter file

```yaml
data:
  src_rec_file_ph: src_rec_file_rotated.csv
  src_rec_file_gr: 
  # src_rec_file: /home/xumijian/Codes/SurfATT/test/00_checkerboard_iso/src_rec_test_all.csv
  iwave: 2 # 1 Love wave (not included in the current version), 2 Rayleigh wave 
  vel_type: [True, False] # use phase velocity, group velocity or both
  weights: [0.5, 0.5] # weights for phase and group velocity

output:
  output_path: OUTPUT_FILES/ # path to save output files
  verbose_level: 2 # 0 quite mode, 1 verbose mode (initial model, temp model for each iteration, kernel density), 2 full output (travel time table)
  log_level: 1 # 0 debug mode, 1 verbose mode

domain:
  depth: [0, 15] # depth range in km
  interval: [0.01, 0.01, 0.5] # x, y, z in km
  num_grid_margin: 5 # number of grid margin

topo:
  is_consider_topo: True # whether consider topography
  topo_file: hawaii_rotated.nc # Path to local elevation file. Only valid in topo_type: 1 and 2
  wavelen_factor: 2.5

inversion:
  # ------- Initial model --------
  init_model_type: 1 # 0: increase from v0 to v1; 1: 1D inversion for average tt; 2: use a 3D vs model
  vel_range: [1.8, 4.2]
  init_model_path: /path/to/init_mod.h5 # Path to initial model. Only valid in init_model_type: 2
  # ------- Regularization --------
  kdensity_coe: 1 # Kdensity_coe is used to rescale the final kernel:  kernel -> kernel / pow(density of kernel, Kdensity_coe).
  ncomponents: 5 # number of multiple grid
  n_inv_grid: [8, 9, 10]
  # ------- Inversion parameters --------
  niter: 40 # max iterations
  min_derr: 0.0001 # minimum error change
  # ------- optimization parameters -------
  optim_method: 2 # 0: SD (adeptive step length); 1: CG (line search); 2: LBFGS (line search)
  step_length: 0.02 # starting step length
  maxshrink: 0.6 # max step length descent
  # ------- Line search for LBFGS -------
  max_sub_niter: 10 # max sub iterations for line search
```
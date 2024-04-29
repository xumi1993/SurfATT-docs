# Tomography

We have prepared 2 or 3 files for the tomography inversion:

- Travel-time data file
- Input parameter file
- Surface topography file (optional)


## Command `surfatt_tomo`

The `surfatt_tomo` command performs the surface wave tomography inversion based on the travel-time data and input parameter files. The surface topography file is optional and can be used to consider the topography effect in the inversion. The command is called as follows:

```{code-block} console
 Usage: surfatt_tomo -i para_file [-f] [-h]
 
 Adjoint-state travel time tomography for surface wave
 
 required arguments:
  -i para_file  Path to parameter file in yaml format
 
 optional arguments:
  -f            Forward simulate travel time for surface wave instead of inversion, defaults to False
  -h            Print help message
```

## Example

In the previous sections, we have prepared the travel-time data file `src_rec_file_ph.csv`, the input parameter file `input_params.yml` and the topography file `hawaii_rotated.nc`. We can now perform the surface wave tomography inversion using the `surfatt_tomo` command under 8 processes:

```bash
mpirun -np 8 surfatt_tomo -i input_params.yml
```

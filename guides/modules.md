## Pre-installed software 

`modulefiles` or `lmod` are two tools that can be find anywhere in HPC installations, either on-prem or in the cloud. Both have the objective to allow users to customise the environment and easily switch across versions and flavours of multiple compilers, libraries, applications usually pre-installed in the system by a sysadmin or a support specialist. 

If the software you need is not pre-installed, there are three options:
* Install it manually locally (suggested)
* Install it locally using spack
* Ask and we will install it centrally for you

##### Basic modulefile commands

For who is not familiar with mofulefile, here a short explanation of the most useful and common commands:
* `module avail` : show all modules present in the system
* `module load my-module` : load a specific `my-module` file, automatically changing user environment to point to the right location of binaries and libraries 
* `module unload my-module` : unload a specific `my-module` file, restoring user environment prior the load operation
* `module list` : list all the modules that have been loaded
* `module show my-module` : show what changed the module will apply to the user envrionment
* `module purge` : unload all loaded modules at once, restoring the user environment like it was fisrt login. It does not revert changes done manually (e.g. using explicit `export`)

##### Pre-installed modules

###### Compilers

| Software  | Module name  | Notes |
|---|---|---|
| GNU 12.3.0 | `gcc/12.3.0-gcc-7.3.1-jttj24nz`  | Support `neoverse_v1` u-arch  |
| NVIDIA HPC SDK 23.9 | `nvhpc/23.9-gcc-12.3.0-zb6fx5p`  |  Provide basic BLAS and LAPACK |
| ARM Compiler for Linux (ACfl) | `acfl/23.10-gcc-12.3.0-6gfsn34`  | Provide Arm Performance Libraries (ArmPL) for ACfl |

###### Math libraries

| Software  | Module name  | Notes |
|---|---|---|
| ArmPL for GNU |  `armpl-gcc/23.10_gcc-12.2-gcc-12.3.0-ihentrd` | Provided Arm Performance Libraries (ArmPL) for GNU |
| ArmPL for NVHPC  | `armpl/23.10.0_nvhpc-23.3` |  Does automatically load `nvhpc` |
| FFTW 3.3.10 for GNU | `fftw/3.3.10-gcc-12.3.0-iecd6zg` | No MPI support, yes threading |
| OpenBLAS 0.3.24 for GNU | `openblas/0.3.24-gcc-12.3.0-txttsng` | Yes threading (OpenMP) |

###### MPI libraries

| Software  | Module name  | Notes |
|---|---|---|
| OpenMPI 4.x for GNU | `openmpi/4.1.6-gcc-12.3.0-tan4tif`  |   |  Uses librabric |
| OpenMPI 4.x for NVIDIA HPC SDK | `openmpi/4.1.6-nvhpc-23.9-jjsxmay`  | Uses librabric |
| OpenMPI 4.x for ARM Compiler | `openmpi/4.1.6-arm-23.10-62sp2ey`  | Uses librabric |


###### Tools & Interpreters

| Software  | Module name  | Notes |
|---|---|---|
| PAPI 7.0.1 | `papi/7.0.1-gcc-12.3.0-wpf7vt7` | | 
| TAU 2.33 for GNU | `tau/2.33-gcc-12.3.0-m4sxxjt` | |
| mpiP 3.5 for GNU | `mpip/3.5-gcc-12.3.0-nswnopt` | | 
| Linaro Forge | `forge/23.0.4` | CLI-only  |
| Python | ` python/3.9.18-gcc-12.3.0-h2xalxe` | |

##### Notes and Best Practices 

If a specific modulefile requires dependencies, those will be loaded automatically. Do check with `module list` if in doubt. Do avoid to load conflicting versions
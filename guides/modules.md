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
| GNU 12.3.0 | `gcc/12.3.0-gcc-8.5.0-xaprqz4`  | Support `neoverse_v1` u-arch  |
| NVIDIA HPC SDK 23.11 | `nvhpc/23.11-gcc-8.5.0-uqgqvs3`  |  Provide basic BLAS and LAPACK |
| ARM Compiler for Linux (ACfl) | `acfl/23.10-gcc-8.5.0-xv7i4dq`  | Provide Arm Performance Libraries (ArmPL) for ACfl |

###### Math libraries

| Software  | Module name  | Notes |
|---|---|---|
| ArmPL for GNU |  `armpl-gcc/23.10_gcc-12.2-gcc-12.3.0-ihentrd` | Provided Arm Performance Libraries (ArmPL) for GNU |
| FFTW 3.3.10 for GNU | `fftw/3.3.10-gcc-12.3.0-dblyinz` | No MPI support, yes threading |

###### MPI libraries

| Software  | Module name  | Notes |
|---|---|---|
| OpenMPI 4.x for GNU | `openmpi/4.1.6-gcc-12.3.0-tntpok2`  |   |  Uses librabric |
| OpenMPI 4.x for ARM Compiler | `openmpi/4.1.6-arm-23.10-jy6uos3`  | Uses librabric |


###### Tools & Interpreters

| Software  | Module name  | Notes |
|---|---|---|
| PAPI (master git)) | `papi/7.1.0-gcc-12.3.0-n2nf2jw` | | 
| TAU 2.33 for GNU | `tau/2.33-gcc-12.3.0-4hviwlh` | |
| mpiP 3.5 for GNU | `mpip/3.5-gcc-12.3.0-nswnopt` | | 

##### Notes and Best Practices 

If a specific modulefile requires dependencies, those will be loaded automatically. Do check with `module list` if in doubt. Do avoid to load conflicting versions
# Perf Libs Tools

[Perf-libs-tools](https://github.com/ARM-software/perf-libs-tools) is logging library designed to measure the calls to maths library functions.
This is used to count the number and type of calls to common BLAS / LAPACK and FFT routines.

This information is collected to help improve maths library performance in the future, by identifying the characteristics of different applications.


## Prerequisites

Perf-libs-tools assumes that you have linked your application with a shared library, any library will do (`armpl`, `openblas`, etc).

### Building the Code

Building Perf-libs-tools is easy, just clone the repo and run make.

```
git clone https://github.com/ARM-software/perf-libs-tools.git
cd perf-libs-tools
make
```

However, there are some steps for 'known issues' you may want to follow:
* Set the `CC=` entry in `Makefile` to your compiler of choice
* Remove the `#include <xblas>` in `src/armpl.h`
* Remove the first 4 lines from `src/PROTOTYPES`

## Using Perf-libs-tools

Perf-libs tools is simple to use, you simply `LD_PRELOAD` the library on the execution line.

We have two main considerations for which library to use:
* Is the package using OpenMP: `libarmpl_mp-summarylog.so`
* Or no OpenMP: `libarmpl-summarylog.so`

Then we simply load the library before our run:
```
export LD_PRELOAD=/<path to install>/lib/libarmpl_mp-summarylog.so
export OMP_NUM_THREADS=8
mpirun -np 4 --map-by slot:PE=8 ./app
```

### Output

This will generate a number of files (default location is `/tmp/armplsummary_<pid>.apl`) with the trace information.

The location can be controlled via the `ARMPL_LOGGING_FILEROOT` environment variable.

These files on their own are very useful.

Examples can be seen in the following two files for a 2 rank MPI run:
* [06422.apl](plt_out/06422.apl)
* [06423.apl](plt_out/06423.apl)


**Note:** Perf-libs-tools will generate one file per process, if you are using only MPI then one file per rank, however with OpenMP this is one file per thread.

### Summary

Whilst these individual files are useful we can also summarize them.

```
python3 tools/process_summary.py *.apl > summary.log
```

This will output merged analysis from all of the files provided.

An example of this output is provided for [06422.apl](plt_out/06422.apl) and [06423.apl](plt_out/06423.apl).

```
Process full dataset for BLAS, LAPACK and FFT function usage.
Opening file plt_out/06422.apl
Opening file plt_out/06423.apl
BLAS level 1     : count      52867    total time       0.0216  user count      47106  user time       0.0203
BLAS level 2     : count      19892    total time       0.0118  user count      16146  user time       0.0108
BLAS level 3     : count      16059    total time       0.0196  user count      16059  user time       0.0196
LAPACK           : count      69601    total time       0.1396  user count      13708  user time       0.0759
FFT              : count        152    total time       0.0035  user count        136  user time       0.0026
 
Double precision : count     158383    total time       0.1893  user count      92975  user time       0.1229
Single precision : count          0    total time       0.0000  user count          0  user time       0.0000
Double complex   : count        112    total time       0.0050  user count        112  user time       0.0050
Single complex   : count          0    total time       0.0000  user count          0  user time       0.0000
 ```
# mpiP

[mpiP](https://github.com/LLNL/mpiP) is a light-weight profiling library for MPI applications. Because it only collects statistical information about MPI functions, mpiP generates considerably less overhead and much less data than tracing tools. All the information captured by mpiP is task-local. It only uses communication during report generation, typically at the end of the experiment, to merge results from all of the tasks into one output file.


## Prerequisites

mpiP intercepts MPI calls at link time.  You can either compile your code with mpiP, or set the `LD_PRELOAD` environment variable at runtime.
In any case, it is recommended to build your code with debugging symbols.

## Using mpiP

mpiP foir gNU 12.3.0 is accessible by type the following: `mpip/3.5-gcc-12.3.0-nswnopt`

mpiP is simple to use. Simply `LD_PRELOAD` the library on the execution line.
You pass options to mpiP by setting the `MPIP` environment variable.
Example:

```
export MPIP="-f output_dir"
export LD_PRELOAD=/<path to install>/lib/libmpiP.so
export OMP_NUM_THREADS=8
mpirun -np 4 --map-by slot:PE=8 ./app
```

### Output

mpiP will generate a report in a text file. Since it captures all information 
about MPI execution, the file can be very lenghty and packed of informations.


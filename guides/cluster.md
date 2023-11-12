## Arm-based AWS Virtual Cluster

This event will take place on virtual clusters hosted on AWS. The main focus will be the Arm based Graviton3 instances. You will have a cluster of the 64-core nodes, with enhanced (EFA) networking.

Each participant will receive a username and password at the beginning odf the tutorial. This will be communicated by voice or via Slack. We advise to change the password at first login. The cluster hostname is **training.day1hpc.com**

On the clusters we have a number of file systems mounted in different folders, for different purposes.

* **`/shared/home`** : Home folders of the users, NFS export mounted on the compute nodes
* **`/shared/home/sw`** : Extra software installs not provided by spack, NFS export mounted on the compute nodes
* **`/shared/work`** : High performance Lustre FS for Spack installs and user runs
* **`/tmp`** : Node local temp storage

#### Job scheduler: Slurm

The clusters are configured to run the `Slurm` scheduler, a common HPC scheduler that many will already be familiar with. For those new to Slurm this [Quick Start User Guide](https://slurm.schedmd.com/quickstart.html) may be useful.

#### Job submission

The Arm Cluster has only queue configured - `graviton`.
```
$ sinfo
PARTITION AVAIL  TIMELIMIT  NODES  STATE NODELIST
graviton*    up    4:00:00     32  idle~ graviton-dy-nodes-[1-32]
```

There are multiple options of job submission, but our simpliest option is via the `srun` command. This command takes as arguement a script, which it will execute on the desired resource.
```
srun -N 1 -n 64 -l hostname 
```

This will submit a job, that will spin up a compute node instance and run the `hostname` command. This command will perform this as an interactive command, and will not return until the job has finished.

#### Batch jobs

For longer lasting jobs, or queuing, then a batch submission is more appropriate.

Prepare a submission script (e.g. name `example.sh`)
```
#!/bin/bash

srun -l hostname
```

On the console do the following:
```
chmod +x example.sh
sbatch -N 1 -n 64 -p graviton example.sh
```
This command tells `Slurm` to run our `example.sh` script on 1 Node, with 64 cores, on partition "graviton".
This will generate output files (`*.err` and `*.out`) in the current directory, named by the job ID, e.g. `slurm-7.out`.

If your job is queued then you can use the `squeue` command to view its status.

#### Interactive Jobs

In addition to the commands above we can use `srun` to provide us an interactive bash shell, this allows us to run multiple commands all within the same environment of a job, without the need for a job submission script. This can be very usefull for debugging purposes or long compilation steps.
```
srun -N 1 -n 64 -p graviton -t 1:00:00 --pty bash
```
############
Using Slurm
############

User access compute nodes for running their work using batch or interactive jobs. 
Nightingale uses the `Slurm job control
software <https://slurm.schedmd.com/documentation.html>`__ to run jobs.
Slurm was developed at California-based DoE labs, and is now perhaps the
most-used job control system on HPC systems in the world. 

If you want to do something that this page doesn't cover with your jobs, feel free to
submit a ticket, but you could also google "how X with slurm" and that
should get you close, as long as you keep in mind the configuration of
the nodes on Nightingale.

Please be aware that the login node is a shared resource for all users of the system 
and using it should be limited to editing, compiling and building your programs, 
and for short non-intensive runs.

To ensure the health of the batch system and scheduler users should refrain from having 
more than 1,000 batch jobs in the queues at any one time.
See the document “Running Serial Jobs Efficiently on Nightingale” regarding information 
on expediting job turnaround time for serial jobs.
See the Running MATLAB / Mathematica Batch Jobs sections for information on running MATLAB 
and Mathematica on Nightingale.

Running Programs
================

If you build your own programs, compiling and linking, an executable is created that is used to run the program. 
If your program is a serial code, you run it by specifying the name of the executable (./a.out).

If you want to run multiple copies of a program you can use the srun command followed by the name of the executable. 
Note: The total number of copies is the {number of nodes} x {cores/node} set in the batch job resource specification. (srun ./a.out)

OpenMP programs are run by setting the number of threads and then specifying the name of the executable. The OMP_NUM_THREADS environment variable is set to specify the number of threads used by OpenMP programs. If this variable is not set, the number of threads used defaults to one under the Intel compiler. Under GCC, the default behavior is to use one thread for each core available on the node. (./a.out)

Managing your jobs with Slurm
=============================

Generally you'll use these commands to run **batch** jobs. Each batch
job is controlled by a script that you hand off and the compute nodes
run when there's enough nodes available to run. That is, the job will
generally run **asynchronously**, so you can log back in and see the
output when it's finished. For more detailed information, refer to the individual man pages.

sbatch
------

Batch jobs are submitted through a job script using the sbatch command. Job scripts generally start with a series of SLURM directives that describe requirements of the job such as number of nodes, wall time required, etc… to the batch system/scheduler (SLURM directives can also be specified as options on the sbatch command line; command line options take precedence over those in the script). The rest of the batch script consists of user commands.

Sample batch scripts are available in the directory /path/to/batch_scripts/

The syntax for sbatch is:
sbatch [list of sbatch options] script_name
The main sbatch options are listed below. Also See the sbatch man page for options.
•	The common resource_names are:
  time=time
  
time=maximum wall clock time (d-hh:mm:ss) [default: maximum limit of the queue(partition) submitted to]

  nodes=n
  ntasks=p Total number of cores for the batch job
  ntasks-per-node=p Number of cores per node
  
n=number of 64-core nodes [default: 1 node]
p=how many cores(ntasks) per job or per node(ntasks-per-node) to use (1 through 64) [default: 1 core]

Examples:
  time=00:30:00
  nodes=2
  ntasks=32

or

  time=00:30:00
  nodes=2
  ntasks-per-node=16

Memory needs: The compute nodes have memory configurations of 256GB, 512GB or 1TB.  The memory configurations are specific to the particular Nightingale queues. Please check the table above to determine what memory configurations are available for the compute nodes associated with the specific queue (partition).

Example:
  time=00:30:00
  nodes=2
  ntask=32
  mem=118000

or

  time=00:30:00
  nodes=2
  ntasks-per-node=16
  mem-per-cpu=7375

Note: Do not use the memory specification unless absolutely required since it could delay scheduling of the job; also, if nodes with the specified memory are unavailable for the specified queue the job will never run.

Accessing the GPUs: To gain access to the GPUs within the batch job’s environment, add the resource specification tesla_a40 (for Tesla A40) or tesla_a100 (for Tesla A100) to your batch script or on the batch job’s submission line.

Example:
(in a batch script)
#SBATCH   gres=gpu:tesla_a40

(on the batch job submission line)
sbatch … --gres=gpu:tesla_a40 batchscript_name.sbatch

**Useful Batch Job Environment Variables**

- **$SLURM_JOB_ID**    Job identifier assigned to the job
- **$SLURM_SUBMIT_DIR**	  By default, jobs start in the directory the job was submitted from.
- **$SLURM_NODELIST**	 variable name that containins the list of nodes assigned to the batch job

See the sbatch man page for additional environment variables available.

srun
----

The srun command initiates an interactive job on the compute nodes.

For example, the following command:
..

[ng-login01 ~]$ srun --partition=cpu --time=00:30:00 --nodes=1 --ntasks-per-node=16 --pty /bin/bash

will run an interactive job in the cpu queue with a wall clock limit of 30 minutes, using one node and 16 cores per node. You can also use other sbatch options such as those documented above.

After you enter the command, you will have to wait for SLURM to start the job. As with any job, your interactive job will wait in the queue until the specified number of nodes is available. If you specify a small number of nodes for smaller amounts of time, the wait should be shorter because your job will backfill among larger jobs. You will see something like this:

srun: job 123456 queued and waiting for resources

Once the job starts, you will see:

srun: job 123456 has been allocated resources

and will be presented with an interactive shell prompt on the launch node. At this point, you can use the appropriate command to start your program.

When you are done with your runs, you can use the exit command to end the job.

Commands that display the status of batch jobs.
-----------------------------------------------

**squeue -a**    List the status of all jobs on the system.

**squeue -u $USER**    List the status of all your jobs in the batch system.

**squeue -j JobID**    List nodes allocated to a running job in addition to basic information.

**scontrol show job JobID**    List detailed information on a particular job.

**sinfo -a**    List summary information on all the queues.

See the man page for other options available.

scancel
-------

The scancel command deletes a queued job or kills a running job.
•	scancel JobID deletes/kills a job.


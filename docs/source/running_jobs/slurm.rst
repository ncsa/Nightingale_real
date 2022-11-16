############
Using Slurm
############

User access compute nodes for running their work using batch or interactive jobs. 
Nightingale uses the `Slurm job control
software <https://slurm.schedmd.com/documentation.html>`__ to run jobs.
Slurm was developed at California-based DoE labs, and is now perhaps the
most-used job control system on HPC systems in the world. 


Please be aware that the login node is a shared resource for all users of the system 
and using it should be limited to editing, compiling and building your programs, 
and for short non-intensive runs.

To ensure the health of the batch system and scheduler users should refrain from having 
more than 1,000 batch jobs in the queues at any one time.


Running Programs
================

On successful building (compilation and linking) of your program, an executable is created that is used to run the program. The table below describes how to run different types of programs.



.. role:: raw-html(raw)
    :format: html

.. list-table:: 
   :widths: 25 25 50
   :header-rows: 1

   * - Program Type
     - How to run the program/executable
     - Example Command
   * - :raw-html:`<br />` Serial :raw-html:`<br />`
       :raw-html:`&nbsp`
     - :raw-html:`<br />` To run serial code, specify the name of the executable.
     - :raw-html:`<br />` ``./a.out``
   * - :raw-html:`<br />` OpenMP :raw-html:`<br />`
     - :raw-html:`<br />` The *OMP_NUM_THREADS* environment variable can be set to
       :raw-html:`<br />` specify the number of threads used by OpenMP programs.
       :raw-html:`<br />` If this variable is not set, the number of threads used
       :raw-html:`<br />` defaults to number of cores available on the node.
       
       To run OpenMP programs, specify the name of the executable.
     - :raw-html:`<br />` ``export OMP_NUM_THREADS=16``
       :raw-html:`<br />` :raw-html:`&nbsp`
       :raw-html:`<br />` :raw-html:`&nbsp`
       :raw-html:`<br />` :raw-html:`&nbsp`
 
       ``./a.out``



:raw-html:`<br />` If you want to run multiple copies of a program you can use the *srun* command followed by the name of the executable. 
:raw-html:`<br />` :raw-html:`&nbsp`
:raw-html:`<br />` Ex. 
:raw-html:`<br />` :raw-html:`&nbsp` :raw-html:`&nbsp` :raw-html:`&nbsp` ``srun ./a.out``
:raw-html:`<br />` :raw-html:`&nbsp`
:raw-html:`<br />` **Note:** By default the total number of copies run, is equal to number cores specified in the batch job resource specification.
:raw-html:`<br />` :raw-html:`&nbsp`
:raw-html:`<br />` Users can use the *-n*  flag/option with the *srun* command to specify the number of copies of a program that they would like to run 
:raw-html:`<br />` keeping in mind that the value for the *-n*  flag/option must be less than or equal to the number of cores specifed for the batch job.
:raw-html:`<br />` :raw-html:`&nbsp`
:raw-html:`<br />` Ex. 
:raw-html:`<br />` :raw-html:`&nbsp` :raw-html:`&nbsp` :raw-html:`&nbsp` ``srun -n 10 ./a.out``
:raw-html:`<br />` :raw-html:`&nbsp`

Managing your jobs with Slurm
=============================

Generally you'll use these commands to run **batch** jobs. Each batch
job is controlled by a script that you hand off and the compute nodes
run when there's enough nodes available to run. That is, the job will
generally run **asynchronously**, so you can log back in and see the
output when it's finished. For more detailed information, refer to the individual man pages.

sbatch
------

Batch jobs are submitted through a *job script* using the ``sbatch`` command. Job scripts generally start with a series of SLURM directives that describe requirements of the job such as number of nodes, wall time required, etc… to the batch system/scheduler (SLURM directives can also be specified as options on the sbatch command line; command line options take precedence over those in the script). The rest of the batch script consists of user commands.

Sample batch scripts are available on Nightingale in the directory ``/sw/apps/NUS/slurm/sample/batchscripts``.

The syntax for **sbatch** is:
:raw-html:`<br />` :raw-html:`&nbsp` ``sbatch [list of sbatch options] script_name``
:raw-html:`<br />` 
:raw-html:`<br />` The main sbatch options are listed below. Also, see the sbatch man page for options.

:raw-html:`<br />` The common resource_names are:
:raw-html:`<br />`
:raw-html:`<br />` :raw-html:`&nbsp` :raw-html:`&nbsp` ``--time=time`` time=maximum wall clock time (d-hh:mm:ss) [default: 30 minutes]
:raw-html:`<br />` :raw-html:`&nbsp` :raw-html:`&nbsp` ``--nodes=n``  Total number of nodes for the batch job
:raw-html:`<br />` :raw-html:`&nbsp` :raw-html:`&nbsp` ``--ntasks=p`` Total number of cores for the batch job
:raw-html:`<br />` :raw-html:`&nbsp` :raw-html:`&nbsp` ``--ntasks-per-node=p`` Number of cores per node
  
:raw-html:`<br />` n=number of 64-core nodes *[default: 1 node]*
:raw-html:`<br />` p=how many cores(ntasks) per job or per node(ntasks-per-node) to use (1 through 64) *[default: 1 core]*

:raw-html:`<br />` Example:
  :raw-html:`&nbsp` ``--time=00:30:00``
  :raw-html:`<br />` :raw-html:`&nbsp` ``--nodes=2``
  :raw-html:`<br />` :raw-html:`&nbsp` ``--ntasks=32``
or
  :raw-html:`&nbsp` ``--time=00:30:00``
  :raw-html:`<br />` :raw-html:`&nbsp` ``--nodes=2``
  :raw-html:`<br />` :raw-html:`&nbsp` ``--ntasks-per-node=16``

Memory needs: The compute nodes have memory configurations of 256GB, 512GB or 1TB.  The memory configurations are specific to the particular Nightingale queues.

:raw-html:`<br />` Example:
  :raw-html:`&nbsp` ``--time=00:30:00``
  :raw-html:`<br />` :raw-html:`&nbsp` ``--nodes=2``
  :raw-html:`<br />` :raw-html:`&nbsp` ``--ntasks=32``
  :raw-html:`<br />` :raw-html:`&nbsp` ``--mem=118000``
or
  :raw-html:`&nbsp` ``--time=00:30:00``
  :raw-html:`<br />` :raw-html:`&nbsp` ``--nodes=2``
  :raw-html:`<br />` :raw-html:`&nbsp` ``--ntasks-per-node=16``
  :raw-html:`<br />` :raw-html:`&nbsp` ``--mem-per-cpu=7375``

Note: Do not use the memory specification unless absolutely required since it could delay scheduling of the job; also, if nodes with the specified memory are unavailable for the specified queue the job will never run.

Accessing the GPUs: To gain access to the GPUs within the batch job’s environment, add the resource specification **tesla_a40** (for Tesla A40) or **tesla_a100** (for Tesla A100) to your batch script or on the batch job’s submission line.


:raw-html:`<br />` Example:
  :raw-html:`&nbsp` (in a batch script)
  :raw-html:`<br />` :raw-html:`&nbsp` ``#SBATCH   gres=gpu:tesla_a40``
or
  :raw-html:`&nbsp` (on the batch job submission line)
  :raw-html:`<br />` :raw-html:`&nbsp` ``sbatch … --gres=gpu:tesla_a40 batchscript_name.sbatch``
  :raw-html:`<br />` :raw-html:`&nbsp`
  :raw-html:`<br />` :raw-html:`&nbsp`


**Useful Batch Job Environment Variables**

.. list-table:: 
   :widths: 25 25 50
   :header-rows: 1
   
   * - Description
     - SLURM Environment Variable
     - Detail Description
   * - :raw-html:`<br />` JobID :raw-html:`<br />`
       :raw-html:`&nbsp`
     - :raw-html:`<br />` ``$SLURM_JOB_ID``
     - :raw-html:`<br />` Job identifier assigned to the job
   * - :raw-html:`<br />` Job Submission Directory :raw-html:`<br />`
       :raw-html:`&nbsp`
     - :raw-html:`<br />` ``$SLURM_SUBMIT_DIR``
     - :raw-html:`<br />` By default, jobs start in the directory the job was submitted from.
   * - :raw-html:`<br />` Machine(node) list :raw-html:`<br />`
       :raw-html:`&nbsp`
     - :raw-html:`<br />` ``$SLURM_NODELIST``
     - :raw-html:`<br />` variable name that containins the list of nodes assigned to the batch job


See the sbatch man page for additional environment variables available.

srun
----

The srun command initiates an interactive batch job on the compute nodes.

For example, the following command:
::

  [ng-login01 ~]$ srun --account=ACCT_NAME --partition=cpu --time=00:30:00 --nodes=1 --ntasks-per-node=16 --pty /bin/bash

(where *ACCT_NAME* is the actual name of your charge account) will run an interactive batch job in the cpu partition (queue) with a wall clock limit of *30 minutes*, using *one node* and *16 cores per node*. You can also use other sbatch options such as those documented above.

After you enter the command, you will have to wait for SLURM to start the job. As with any job, your interactive job will wait in the queue until the resources your reqested for your batch job become available.  If you specify a small number of nodes for smaller amounts of time, the wait should be shorter because your job will backfill among larger jobs. You will see output similar to this:
::

  srun: job 123456 queued and waiting for resources





Once the job starts, you will see:
::

  srun: job 123456 has been allocated resources

and will be presented with an interactive shell prompt on the launch node. At this point, you can use the appropriate command to start your program.

When you are done with your runs, you can use the **exit** command to end the job.

squeue
------

The *squeue* command is used to pull up information about the batch jobs submitted
to the batch system.  By default, the *squeue* command will print out the job ID, 
partition, username, job status, number of nodes, and name of nodes for all batch
jobs queued or running within batch system.

**Commands that display the status of batch jobs**

.. list-table:: 
   :widths: 25 50
   :header-rows: 1
   
   * - SLURM Command
     - Descriptiton
   * - :raw-html:`<br />` ``squeue -a`` :raw-html:`<br />`
       :raw-html:`&nbsp`
     - :raw-html:`<br />` List the status of all batch jobs in the batch system.
   * - :raw-html:`<br />` ``squeue -u $USER`` :raw-html:`<br />`
       :raw-html:`&nbsp`
     - :raw-html:`<br />` List the status of all your batch jobs in the batch system.
   * - :raw-html:`<br />` ``squeue -j JobID`` :raw-html:`<br />`
       :raw-html:`&nbsp`
     - :raw-html:`<br />` List nodes allocated to a specific running batch job in addition to basic information.
   * - :raw-html:`<br />` ``scontrol show job JobID`` :raw-html:`<br />`
       :raw-html:`&nbsp`
     - :raw-html:`<br />` List detailed information on a particular batch job.

Run the command ``man squeue`` to see the other available options.


sinfo
-----

The *sinfo* command is used to view partition and node information for a system running Slurm.

.. list-table:: 
   :widths: 25 50
   :header-rows: 1
   
   * - SLURM Command
     - Descriptiton
   * - :raw-html:`<br />` ``sinfo -a`` :raw-html:`<br />`
       :raw-html:`&nbsp`
     - :raw-html:`<br />` List summary information on all the partitions (queues).

Run the command ``man sinfo`` to see the other available options.


scancel
-------

The *scancel* command deletes a queued job or kills a running job.

.. list-table:: 
   :widths: 35 50
   :header-rows: 1
   
   * - SLURM Command
     - Descriptiton
   * - :raw-html:`<br />` ``scancel JobID`` :raw-html:`<br />`
       :raw-html:`&nbsp`
     - :raw-html:`<br />` To delete/kill a specific batch job
   * - :raw-html:`<br />` ``scancel JobID01, JobID02`` :raw-html:`<br />`
       :raw-html:`&nbsp`
     - :raw-html:`<br />` To delete/kill multiple batch jobs, use a comma-separated list of JobIDs 
   * - :raw-html:`<br />` ``scancel -u $USER`` :raw-html:`<br />`
       :raw-html:`&nbsp`
     - :raw-html:`<br />` To delete/kill all your batch jobs (removes all of your batch jobs from the batch system regardless of the batch job's state) 
   * - :raw-html:`<br />` ``scancel --name JobName`` :raw-html:`<br />`
       :raw-html:`&nbsp`
     - :raw-html:`<br />` To delete/kill multiple batch jobs based on the batch job's name

Run the command ``man scancel`` to see the other available options.



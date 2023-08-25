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

This page is meant to teach you how to put together a job on
Nightingale, submit it to the Nightingale job system, monitor the job
before it runs, during its run, after it has finished, and then how to
retrieve the results. Please see the batch scripts below for working 
examples that can be submitted on Nightingale. Additionally, the batch 
scripts can be copied and modified to suit your specific needs.





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



Nightingale Queues
==================

    
The current limits in the Nightingale queues are below:

================  ==========  ============  =======   ================  ============
Queue(partition)  CPUs        Memory        Max #     GPUs              Max Walltime
                  (per Node)  (per Node)    Nodes     Type : Count
                                                      (per node)
cpu               64	      1TB           16        n/a               7 days
a40               64	      512GB         2         Tesla A40 : 1     7 days
a100              64	      256GB         5         Tesla A100 : 1    7 days
a100x2            64	      512GB         1         Tesla A100 : 2    7 days
================  ==========  ============  =======   ================  ============

The information here and the example scripts assume that you have a working
knowledge of how to write and test a script, and you have a general understanding
of how jobs work. If you don't, but you want to run software on compute nodes, 
the safest place to start is probably interactive batch jobs (below).  Please send
us a ticket if you need help with this.


Managing your jobs with Slurm
=============================

Generally you'll use these commands to run **batch** jobs. Each batch
job is controlled by a script that you hand off and the compute nodes
run when there's enough nodes available to run. That is, the job will
generally run **asynchronously**, so you can log back in and see the
output when it's finished. For more detailed information, refer to the
individual man pages.

sbatch
------

Batch jobs are submitted through a *batch script* using the ``sbatch``
command. Batch scripts generally start with a series of SLURM directives
that describe requirements of the job such as number of nodes, wall time
required, etc… to the batch system/scheduler (SLURM directives can also
be specified as options on the sbatch command line; command line options
take precedence over those in the script). The rest of the batch script
consists of user commands.


The syntax for submitting a batch job with **sbatch** is:
::

  sbatch [list of sbatch options] script_name


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
  :raw-html:`&nbsp` ::

  #SBATCH   --gres=gpu:tesla_a40

or
  :raw-html:`&nbsp` (on the batch job submission line)
  :raw-html:`&nbsp` ::

   sbatch … --gres=gpu:tesla_a40 batchscript_name.sbatch

  


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

System Reservations
--------------------

Please note, the system will periodically be unavailable to start jobs. 
There are 3 scheduled system maintenance periods every year in January, 
May, and August. Other unscheduled, emergency downtimes may occur for 
important system software security updates or due to a hardware failure.
If there is a downtime there will be a reservation in SLURM to prevent 
jobs from starting if they would not be complete before the interruption 
begins.

If a reservation is blocking your job from starting the squeue command 
will show a message like (ReqNodeNotAvail, Reserved for maintenance) 
for your job. You can shorten the runtime of your job to fit in before 
the reservation starts to avoid the reservation.

When you log into Nightingale any upcoming system interruptions are 
listed in the message of the day.

Sample Batch Scripts
--------------------

When using Slurm to run your software on the Nightingale compute
nodes, job instructions and run commands are organized into a
"batch script". This page gives you hints about composing your own batch
scripts for Slurm on Nightingale, and it also has some basic batch scripts
you may copy and use as templates for your own batch scripts. To use the
examples on this page, we assume that you generally know how to write a
shell scripts and how they work.

By default, when your batch script is run, it has copies of all the
environment variables that existed in your shell when you submit (sbatch-ed)
the batch script to the SLURM batch system. You can control the job behavior
this way.

Below is a sample batch script that just runs a single serial application
(hostname). Hostname is not an application that you'd normally run; it's
here because it's a harmless example that does something very quickly
and then exits. If you run this script, though, and it works, then you
know that you have a working script and you can build from there.
Typically you'd replace "hostname" which some application code that you
wanted to run to do work on the compute node.

::

   #!/bin/bash                                                                                                                                                                                               
   ###############################################################################                                                                                                                           
   ##                                                                           ##                                                                                                                           
   ##                   NCSA Nightingale Cluster                                ##                                                                                                                           
   ##                                                                           ##                                                                                                                           
   ##                   Sample SERIAL Job Batch Script                          ##                                                                                                                           
   ##                                                                           ##                                                                                                                           
   ###############################################################################                                                                                                                           

   # To see a list of possible #SBATCH options, run "man sbatch" on the                                                                                                                                      
   # command line.                                                                                                                                                                                           

   # NOTE: option lines that begin with "#SBATCH" (single "#") are active and will                                                                                                                           
   # be read and implemented by slurm as the job is set up.                                                                                                                                                  
   # Lines that begin with "##SBATCH" are considered "commented out" and                                                                                                                                     
   # ignored by slurm.  Both of those are ignored as the job script runs *within*                                                                                                                            
   # the job.                                                                                                                                                                                                

   # the "-A" directive specifies what "allocation account" your job time will                                                                                                                               
   # be charged to.  You will need to replace "usrsvc" with the name of your                                                                                                                                 
   # allocation account                                                                                                                                                                                      
   #                                                                                                                                                                                                         
   #SBATCH -A usrsvc                                                                                                                                                                                         

   # other general job parameters                                                                                                                                                                            
   #SBATCH --time=00:05:00                  # Job run time (hh:mm:ss)                                                                                                                                        
   #SBATCH --nodes=1                        # Number of nodes                                                                                                                                                
   #SBATCH --ntasks-per-node=16             # Number of task (cores/ppn) per node                                                                                                                            
   #SBATCH --job-name=serial_job            # Name of batch job                                                                                                                                              
   #SBATCH --partition=cpu                  # Partition (queue)                                                                                                                                              
   #SBATCH --output=serial_%j.out           # stdout from job is written to this file                                                                                                                        
   #SBATCH --error=serial_%j.err            # stderr from job is written to this file                                                                                                                        
   ##SBATCH --mail-user=NetID@illinois.edu  # put YOUR email address for notifications                                                                                                                       
   ##SBATCH --mail-type=BEGIN,END           # Type of email notifications to send                                                                                                                            
   #                                                                                                                                                                                                         
   ###############################################################################                                                                                                                           
   # Change to the directory from which the batch job was submitted                                                                                                                                          
   # Note: SLURM defaults to running jobs in the directory where                                                                                                                                             
   # they are submitted, no need for cd'ing to $SLURM_SUBMIT_DIR                                                                                                                                             

   echo
   echo "running slurm job on Nightingale on behalf of user ${USER}"
   echo
   echo "running in directory ${SLURM_SUBMIT_DIR}"
   echo

   # Run the serial code                                                                                                                                                                                     
   hostname

| 

The following is a batch script that runs a code in parallel, with a couple of other
features that are useful in batch jobs:

::

   #!/bin/bash
   ###############################################################################
   ##                                                                           ##
   ##                   NCSA Nightingale Cluster                                ##
   ##                                                                           ##
   ##                 Sample PARALLEL Job Batch Script                          ##
   ##                                                                           ##
   ###############################################################################

   # To see a list of possible #SBATCH options, run "man sbatch" on the
   # command line.  

   # NOTE: option lines that begin with "#SBATCH" (single "#") are active and will
   # be read and implemented by slurm as the job is set up.
   # Lines that begin with "##SBATCH" are considered "commented out" and
   # ignored by slurm.  Both of those are ignored as the job script runs *within*
   # the job.  

   # the "-A" directive specifies what "allocation account" your job time will
   # be charged to.  You will need to replace "usrsvc" with the name of your
   # allocation account
   # 
   #SBATCH -A usrsvc                        

   # other general job parameters
   #SBATCH --time=00:05:00                  # Job run time (hh:mm:ss)
   #SBATCH --nodes=1                        # Number of nodes
   #SBATCH --ntasks-per-node=16             # Number of task (cores/ppn) per node
   #SBATCH --job-name=parallel_job          # Name of batch job
   #SBATCH --partition=cpu                  # Partition (queue)           
   #SBATCH --output=parallel_%j.out           # stdout from job is written to this file
   #SBATCH --error=parallel_%j.err            # stderr from job is written to this file
   ##SBATCH --mail-user=NetID@illinois.edu  # put YOUR email address for notifications
   ##SBATCH --mail-type=BEGIN,END           # Type of email notifications to send
   #                                                                            
   ###############################################################################
   # Change to the directory from which the batch job was submitted
   # Note: SLURM defaults to running jobs in the directory where
   # they are submitted, no need for cd'ing to $SLURM_SUBMIT_DIR

   # your job will create a job-specific directory and then run within that
   # directory.  This is handy if your application outputs a lot of files
   # in its local directory and you need to keep them separate by job.  
   MY_JOB_DIR="parallel_job_${SLURM_JOB_ID}"
   mkdir ${MY_JOB_DIR}
   cd ${MY_JOB_DIR}
   # NOTE: stdout and stderr files will still end up in the original directory
   # that you ran sbatch in, not the job-specific subdirectory

   echo 
   echo "running slurm job on Nightingale on behalf of user ${USER}"
   echo 
   echo "running in directory ${SLURM_SUBMIT_DIR}"
   echo 


   # set start time stamp
   touch application_start_time
   # Run the code in parallel across several cores
   srun hostname
   # set end time stamp
   touch application_end_time

| 



Additional sample batch scripts are available on Nightingale in the following directory:
::

  /sw/apps/NUS/slurm/sample/batchscripts



srun (command line)
----
interactive batch job
_____________________

Rather than queuing up a batch job to run on the compute nodes, you can request
that the job scheduler allocate you to a compute node **now**, and to log 
you onto it. These are called interactive batch jobs.

Projects that have dedicated interactive nodes, do not need to go through
the scheduler. Members of these projects just login directly to thier nodes.

To launch an interactive batch job using the job scheduler with the default
values for the job resources(nodes,cores,memory,etc ...), run
the following command:

::

   srun -A usrsvc --pty bash 

(You'll need change "usrsvc" in that command to the name of your
allocation account.)

**Warning**: be sure to end the interactive job as soon as you're done (by typing 
*exit*). If you leave the job running, even if you're not running any processes, 
your allocation account is being charged for the time.


To specify resources for your interactive batch job the 
srun command syntax should look similar to the following:
::

  srun --account=ACCT_NAME --partition=cpu --time=00:30:00 --nodes=1 --ntasks-per-node=16 --pty /bin/bash

(where *ACCT_NAME* is the actual name of your charge account) will run an
interactive batch job in the cpu partition (queue) with a wall clock limit
of *30 minutes*, using *one node* and *16 cores per node*. You can also use
other sbatch options such as those documented above.

After you enter the command, you will have to wait for SLURM to start the
job.  You will see output similar to this:
::

  srun: job 123456 queued and waiting for resources





Once the job starts, you will see:
::

  srun: job 123456 has been allocated resources

and will be presented with an interactive shell prompt on the launch node. At this point, you can use the appropriate command(s) to start your program.

Again, when you are done with your interactive batch job session, you can use the **exit** command to end the job.


srun (batch script)
----

:raw-html:`<br />` Inside a batch script if you want to run multiple copies of a program you can use the *srun* command followed by the name of the executable. 
:raw-html:`<br />` :raw-html:`&nbsp`
:raw-html:`<br />` Ex.
::

  srun ./a.out

:raw-html:`<br />` :raw-html:`&nbsp`
:raw-html:`<br />` **Note:** By default the total number of copies run, is equal to number cores specified in the batch job resource specification.
:raw-html:`<br />` :raw-html:`&nbsp`
:raw-html:`<br />` Users can use the *-n*  flag/option with the *srun* command to specify the number of copies of a program that they would like to run 
:raw-html:`<br />` keeping in mind that the value for the *-n*  flag/option must be less than or equal to the number of cores specifed for the batch job.
:raw-html:`<br />` :raw-html:`&nbsp`
:raw-html:`<br />` Ex. 
::

  srun -n 10 ./a.out

:raw-html:`<br />` :raw-html:`&nbsp`




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
   * - :raw-html:`<br />` ``sinfo -p PRTN_NAME`` :raw-html:`<br />`
       :raw-html:`&nbsp`
     - :raw-html:`<br />` Print information only about the specified partition(s). Multiple partitions are separated by commas.


:raw-html:`<br />` :raw-html:`&nbsp`
Users can view the partitions(queues) that they have the ability to submit batch jobs to, by typing the following command:
::

    [ng-login01 ~]$ sinfo -s -o "%.14R %.12l %.12L %.5D"
    
Users can also view specific configuration information about the compute nodes associated with their primary partition(s), by typing the following command:
::

    [ng-login01 ~]$ sinfo -p queue(partition)_name -N -o "%.8N %.4c %.16P %.9m %.12l %.12L %G"


:raw-html:`<br />` :raw-html:`&nbsp`
Run the command ``man sinfo`` to see the other available options.

:raw-html:`<br />` :raw-html:`&nbsp`

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



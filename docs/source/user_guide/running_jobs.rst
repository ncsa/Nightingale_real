Running Jobs
=========================

Introduction
-------------

.. note::
   Many researchers on Nightingale have access to their own node(s), often called *interactive* nodes, specially dedicated for a group's use. 
   If that's the case for you, then you will be given specific instructions on how to log into your own interactive node in the Nightingale cluster.
   If instead of (or in addition to) access to your own interactive node, you have access to the shared pool of computational (*compute*) nodes that are part of the Nightingale cluster, this page describes how to access them.

The shared pool of compute nodes is called a *batch queue*. 
Jobs you submit to the batch queue wait until there are resources available to run them. 
Contact your principal investigator (PI) to determine if your group has access to the batch queue on Nightingale and find out what account you should use when submitting batch jobs.

The compute *cluster* part of Nightingale is a shared pool of nodes available for running your software. Because there is more than one compute node on Nightingale, if your application can run on more than one computer at a time, it can potentially run faster. 
The batch system can also run your application as part of a *job*, which is a block of instructions that the system will execute when there are compute nodes available to do the work. 
When you have submitted a job, the system will execute the instructions in the job without you having to be logged into Nightingale. 
You can queue up multiple jobs, and they will run sometime while you're away. 
This makes the cluster very efficient at running software that can be broken down into chunks that can each be executed by a job. 
Jobs are typically configured to write their results to a location on disk, so you can retrieve the results when you next log into Nightingale.

Accessing the Compute Nodes
-----------------------------

The *login* node is a shared resource for all users and login node use should be limited to editing, compiling, and building your programs, and for short *non-intensive* runs.
Access *compute* nodes for running your work using *batch* or *interactive* jobs. 
Nightingale uses the `Slurm job control software <https://slurm.schedmd.com/documentation.html>`_ to run jobs. The `Slurm quick start user guide <https://slurm.schedmd.com/quickstart.html>`_ provides a brief overview for new users.

.. note::
   To ensure the health of the batch system and scheduler, avoid having more than **1,000 batch jobs** in the queues at any one time.

Batch scripts (``sbatch``) or Interactive (``srun``), which is right for you?

- :ref:`sbatch` - Use batch scripts for jobs that are debugged, ready to run, and don't require interaction.
  Sample Slurm batch job scripts are provided in the :ref:`examples` section.
  Slurm also supports `job arrays <https://slurm.schedmd.com/job_array.html>`_ for easy management of a set of similar jobs.

- :ref:`srun` - For interactive use of a compute node, ``srun`` will run a single command through Slurm on a compute node. ``srun`` blocks; it will wait until Slurm has scheduled compute resources and when it returns, the job is complete.

Running Programs
------------------

On successful building (compilation and linking) of your program, an executable is created that is used to run the program. The table below describes how to run different program types.

+--------------+------------------------------------------------------------------------------+------------------------------+
| Program Type | How to Run the Program/Executable                                            | Example Command              |
+==============+==============================================================================+==============================+
| Serial       | To run serial code, specify the name of the executable.                      | ``./a.out``                  |
+--------------+------------------------------------------------------------------------------+------------------------------+
| OpenMP       | The ``OMP_NUM_THREADS`` environment variable can be set to specify the       | ``export OMP_NUM_THREADS=16``|
|              |                                                                              |                              |
|              | number of threads used by OpenMP programs. If this variable is not set, the  |                              |
|              |                                                                              |                              |
|              | number of threads used defaults to the number of cores available on the node.|                              |
+              +------------------------------------------------------------------------------+------------------------------+
|              | To run OpenMP programs, specify the name of the executable.                  | ``./a.out``                  |
+--------------+------------------------------------------------------------------------------+------------------------------+

.. _queues:

Nightingale Queues
--------------------
    
The current limits of the Nightingale queues are below:

+------------------+----------------+------------------+------------+------------------------+-------------+
| Queue (partition)| CPUs (per node)| Memory (per node)| Max # Nodes| GPUs                   | Max Walltime|
|                  |                |                  |            |                        |             |
|                  |                |                  |            | Type : Count (per node)|             |
+==================+================+==================+============+========================+=============+
| cpu              | 64             | 1TB              | 16         | n/a                    | 7 days      |
+------------------+----------------+------------------+------------+------------------------+-------------+
| a40              | 64             |512GB             | 2          | Tesla A40 : 1          | 7 days      |    
+------------------+----------------+------------------+------------+------------------------+-------------+
| a100             | 64             | 256GB            | 5          | Tesla A100 : 1         | 7 days      |
+------------------+----------------+------------------+------------+------------------------+-------------+
| a100x2           | 64             | 512GB            | 1          | Tesla A100 : 2         | 7 days      |
+------------------+----------------+------------------+------------+------------------------+-------------+

.. _system-reservations:

System Reservations
---------------------

The system will periodically be unavailable to start jobs. 
**When you log into Nightingale any upcoming system interruptions are listed in the message of the day.**
There are three *scheduled* system maintenance periods every year in January, May, and August. 
Other *unscheduled*, emergency downtimes may occur for important system software security updates or due to a hardware failure.
For a downtime, there will be a reservation in Slurm to prevent jobs from starting if the jobs would not be complete before the downtime begins.

If a downtime reservation is blocking your job from starting, the ``squeue`` command will show a message like ``ReqNodeNotAvail, Reserved for maintenance`` for your job. 
You may be able to shorten the runtime of your job to fit in before the downtime reservation starts.

.. _slurm:

Managing Your Jobs with Slurm
------------------------------

.. note::
   If you are new to writing and testing scripts, and new to jobs, we recommend starting with :ref:`interactive batch jobs <interactive>`. If you need help, please :ref:`submit a support request <help>`.

Generally, you will use the below commands to run *batch* jobs. 
Each batch job is controlled by a script that the compute nodes run when there are enough nodes available. 
That is, the job will generally run *asynchronously*, so you can log back in and see the output when it's finished. 
For more detailed information, refer to the individual command `man pages <https://en.wikipedia.org/wiki/Man_page>`_.

.. _sbatch:

sbatch
~~~~~~~

Batch jobs are submitted through a batch script using the ``sbatch`` command. 
Batch scripts generally start with a series of Slurm directives that describe requirements of the job to the batch system/scheduler, such as number of nodes and walltime. 
Slurm directives can also be specified as options on the ``sbatch`` command line; command line options take precedence over those in the script. 
The rest of the batch script consists of user commands.

The syntax for submitting a batch job with ``sbatch`` is:

.. code-block::

  sbatch [list of sbatch options] script_name

The main ``sbatch`` options are listed below. 

+-------------------------+------------------------------------------------------------------+
| Option                  | Description                                                      |
+=========================+==================================================================+
| ``--time=time``         | time = maximum wall clock time (d-hh:mm:ss) [default: 30 minutes]|
+-------------------------+------------------------------------------------------------------+
| ``--nodes=n``           | Total number of nodes for the batch job.                         |
|                         |                                                                  |
|                         | n = number of 64-core nodes [default: 1 node]                    |
+-------------------------+------------------------------------------------------------------+
| ``--ntasks=p``          | Total number of cores for the batch job.                         |
|                         |                                                                  |
|                         | p = number of cores per job to use (1 - 64) [default: 1 core]    |
+-------------------------+------------------------------------------------------------------+
| ``--ntasks-per-node=p`` | Number of cores per node.                                        |
|                         |                                                                  |
|                         | p = number of cores per node to use (1 - 64) [default: 1 core]   |
+-------------------------+------------------------------------------------------------------+

**Example:**

.. code-block::

   --time=00:30:00 
   --nodes=2 
   --ntasks=32

or 

.. code-block::

   --time=00:30:00 
   --nodes=2 
   --ntasks-per-node=16

See the ``sbatch`` man page for additional information.

Memory needs
$$$$$$$$$$$$$

.. warning::
   Do not use the memory specification unless absolutely required because it could delay scheduling of the job; if nodes with the specified memory are unavailable for the specified queue, the job will *never* run.

The compute nodes have memory configurations of 256GB, 512GB or 1TB.  The memory configurations are specific to the particular :ref:`Nightingale queues <queues>`.

**Example:**

.. code-block::

   --time=00:30:00 
   --nodes=2 
   --ntasks=32 
   --mem=118000

or

.. code-block::

   --time=00:30:00 
   --nodes=2 
   --ntasks-per-node=16 
   --mem-per-cpu=7375

Accessing the GPUs 
$$$$$$$$$$$$$$$$$$$$

To gain access to the GPUs within the batch job’s environment, add the resource specification ``tesla_a40`` (for Tesla A40) or ``tesla_a100`` (for Tesla A100) to your batch script or on the batch job’s submission line.


**Example:**

In the batch script:

.. code-block::

   #SBATCH   --gres=gpu:tesla_a40

In the batch job submission line:

.. code-block::

   sbatch … --gres=gpu:tesla_a40 batchscript_name.sbatch

Useful Batch Job Environment Variables
$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$

========================= =========================== ===================
Description               SLURM Environment Variable  Detail Description
========================= =========================== ===================
JobID                     ``$SLURM_JOB_ID``           Job identifier assigned to the job 
Job Submission Directory  ``$SLURM_SUBMIT_DIR``       By default, jobs start in the directory the job was submitted from.
Machine (node) list       ``$SLURM_NODELIST``         Variable name that contains the list of nodes assigned to the batch job
========================= =========================== ===================

See the ``sbatch`` man page for additional environment variables.

.. _srun:

srun
~~~~~~

.. _interactive:

Command Line
$$$$$$$$$$$$$$$

Instead of queuing up a batch job to run on the compute nodes, you can request that the job scheduler allocate you to a compute node *now* and log you onto it. These are called *interactive batch jobs*. Projects that have dedicated interactive nodes, do not need to go through the scheduler; members of these projects just log in directly to their nodes.

To launch an interactive batch job using the job scheduler with the default values for the job resources (nodes,cores,memory, and so on), run the following command, replacing ``ALL_ACCT``, with the name of your allocation account:

.. code-block::

   srun -A ALL_ACCT --pty bash 

.. warning::
   End the interactive job **as soon as you're done**, by typing ``exit``. If you leave the job running, even if you are not running any processes, your allocation account is being charged for the time.

To specify resources for your interactive batch job the ``srun`` command syntax should look similar to the following, replacing ``ACCT_NAME`` with the name of your charge account:

.. code-block::

  srun --account=ACCT_NAME --partition=cpu --time=00:30:00 --nodes=1 --ntasks-per-node=16 --pty /bin/bash

This example will run an interactive batch job in the CPU partition (queue) with a wall clock limit of **30 minutes**, using **one node** and **16 cores per node**. You can also use other ``sbatch`` options.

After you enter the command, you will have to wait for Slurm to start the job. You will see output similar to:

.. code-block::

   srun: job 123456 queued and waiting for resources

Once the job starts, you will see:

.. code-block::

   srun: job 123456 has been allocated resources

and will be presented with an interactive shell prompt on the launch node. At this point, you can use the appropriate command(s) to start your program.

When you are done with your interactive batch job session, use the ``exit`` command to end the job.

Batch Script
$$$$$$$$$$$$$$

Inside a batch script if you want to run multiple copies of a program you can use the ``srun`` command followed by the name of the executable: 

.. code-block::

   srun ./a.out

By default, the total number of copies run is equal to number of cores specified in the batch job resource specification.
You can use the ``-n``  flag/option with the ``srun`` command to specify the number of copies of a program that you would like to run; the value for the ``-n`` flag/option must be less than or equal to the number of cores specified for the batch job.

.. code-block::

   srun -n 10 ./a.out

squeue
~~~~~~~

The ``squeue`` command is used to pull up information about batch jobs submitted to the batch system. By default, the ``squeue`` command will print out the JobID,  partition, username, job status, number of nodes, and name of nodes for all batch jobs queued or running within batch system.

============================ ============
Slurm Command                Description
============================ ============
``squeue -a``                List the status of all batch jobs in the batch system.
``squeue -u $USER``          List the status of all your batch jobs in the batch system.
``squeue -j JobID``          List nodes allocated to a specific running batch job in addition to basic information.
``scontrol show job JobID``  List detailed information on a particular batch job.
============================ ============

See the ``squeue`` man page for other available options.

sinfo
~~~~~~

The ``sinfo`` command is used to view partition and node information for a system running Slurm.

+------------------------+----------------------------------------------------------+
| Slurm Command          | Description                                              |
+========================+==========================================================+
| ``sinfo -a``           | List summary information on all the partitions (queues). |
+------------------------+----------------------------------------------------------+
| ``sinfo -p PRTN_NAME`` | Print information only about the specified partition(s). |
|                        |                                                          |
|                        | Multiple partitions are separated by commas.             |
+------------------------+----------------------------------------------------------+

View the partitions (queues) that you can submit batch jobs to with the following command:

.. code-block::

    [ng-login01 ~]$ sinfo -s -o "%.14R %.12l %.12L %.5D"
    
View specific configuration information about the compute nodes associated with your primary partition(s) with the following command:

.. code-block::

    [ng-login01 ~]$ sinfo -p queue(partition)_name -N -o "%.8N %.4c %.16P %.9m %.12l %.12L %G"

See the ``sinfo`` man page for other available options.

scancel
~~~~~~~~

The ``scancel`` command deletes a queued job or kills a running job.

+------------------------------+--------------------------------------------------------------------------+
| Slurm Command                | Description                                                              |
+==============================+==========================================================================+
| ``scancel JobID``            | To delete/kill a specific batch job                                      |
+------------------------------+--------------------------------------------------------------------------+
| ``scancel JobID01, JobID02`` | To delete/kill multiple batch jobs, use a comma-separated list of JobIDs |
+------------------------------+--------------------------------------------------------------------------+
| ``scancel -u $USER``         | To delete/kill all your batch jobs (removes all your batch jobs from     |
|                              |                                                                          |
|                              | the batch system regardless of the batch job’s state)                    |
+------------------------------+--------------------------------------------------------------------------+
| ``scancel --name JobName``   | To delete/kill multiple batch jobs based on the batch job’s name         |
+------------------------------+--------------------------------------------------------------------------+

See the ``scancel`` man page for other available options.

.. _examples:

Sample Batch Scripts
----------------------

The below example scripts will give you hints about composing your own batch scripts for Slurm on Nightingale. You can copy and use the examples as templates for your own batch scripts.

By default, when your batch script is run, it has copies of all the environment variables that existed in your shell when you submitted the batch script to the Slurm batch system. You can control the job behavior this way.

Additional sample batch scripts are available on Nightingale in the following directory:

.. code-block::

  /sw/apps/NUS/slurm/sample/batchscripts

Serial Job
~~~~~~~~~~~~~

Below is a sample batch script that runs a single serial application, ``hostname``. (``hostname`` is not an application that you would normally run; we are using it in this example because it's a harmless example that does something very quickly and then exits.) If you run this script, and it works, then you know that you have a working script and you can build/modify from there. Replace ``hostname`` with some application code that you wanted to run to do work on the compute node.

.. raw:: html

   <details>
   <summary><a><b>Sample Serial Job Batch Script</b> <i>(click to expand/collapse)</i></a></summary>

.. code-block::

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

.. raw:: html

   </details>
|

Parallel Job 
~~~~~~~~~~~~~~~~~~~~~~~~~

The following is a batch script that runs a code in parallel with a couple of other features that are useful in batch jobs:

.. raw:: html

   <details>
   <summary><a><b>Sample Parallel Job Batch Script</b> <i>(click to expand/collapse)</i></a></summary>

.. code-block::

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

.. raw:: html

   </details>
| 


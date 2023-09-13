==================================
Sample Job Scripts
==================================

If you're using Slurm to run your software on the Nightingale compute
nodes, then you organize the job instructions and run commands into a
"job script". This page gives you hints about composing your own job
scripts for Slurm on Nightingale, and it also has some basic job scripts
you may copy and use as templates for your own job scripts. To use the
examples on this page, we assume that you generally know how to write a
bash script and how it works.

By default, when your job script is run, it has copies of all the
environment variables that existed in your shell when you sbatch-ed the
script. You can control the job behavior this way.

Here's a sample job script that just runs a single serial application
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

Here's a job that runs a code in parallel, with a couple of other
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

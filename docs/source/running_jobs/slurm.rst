############
Using Slurm
############

Nightingale uses the `Slurm job control
software <https://slurm.schedmd.com/documentation.html>`__ to run jobs.
Slurm was developed at California-based DoE labs, and is now perhaps the
most-used job control system on HPC systems in the world. If you want to
do something that this page doesn't cover with your jobs, feel free to
submit a ticket, but you could also google "how X with slurm" and that
should get you close, as long as you keep in mind the configuration of
the nodes on Nightingale.

Managing your jobs with Slurm
=============================

Generally you'll use these commands to run **batch** jobs. Each batch
job is controlled by a script that you hand off and the compute nodes
run when there's enough nodes available to run. That is, the job will
generally run **asynchronously** , so you can log back in and see the
output when it's finished.

sbatch <my_job_script>
----------------------

submits that script to the job system. It will handle the job according
to the #SBATCH directives in the top of the script (see example
scripts).

squeue
------

This command lists the jobs that are currently running on the system. If
there are lots of jobs, you can run

::

   squeue --user=${USER}
   
to only see **your** jobs.

scancel <jobid>
---------------

This kills a job that is in progress and ends it immediately, without
waiting for any applications to finish.

################
Interactive Jobs
################

Rather than queuing up a job to run on the compute nodes, you can request
that the job scheduler allocate you to a compute node **now**, and to log 
you onto it. These are called interactive jobs.

Some projects have dedicated interactive nodes, users log into
those nodes directly, they don't go through the job scheduler to get to them.

To launch an interactive job using the job scheduler, run
the following command:

::

   srun -A usrsvc --pty bash 

(You'll need change "usrsvc" in that command to the name of your
allocation account.)

Warning: be sure to end the interactive job as soon as you're done. If
you leave the job running, even if you're not running any processes, you
allocation account is being charged for the time.

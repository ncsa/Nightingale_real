################
Interactive Jobs
################

Unlike batch jobs above, you can also ask the scheduler for a compute
node **now** , and to log you onto it. To launch an interactive job, run
the following command:

::

   srun -A usrsvc --pty bash 

(You'll need change "usrsvc" in that command to the name of your
allocation account.)

Warning: be sure to end the interactive job as soon as you're done. If
you leave the job running, even if you're not running any processes, you
allocation account is being charged for the time.

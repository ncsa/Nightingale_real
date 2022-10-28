############
Introduction
############

Many researchers on Nightingale will have access to their own node or
nodes, often called "interactive" nodes. Those specially-dedicated nodes
are for that group's use. If that's the case for you, then you will have
specific instructions on how to log into your own interactive node in
the Nightingale cluster, and you don't have to worry about the
instructions on this page. If instead of (or in addition to) access to
your own interactive node, you have access to the shared pool of
computational ("compute") nodes that are part of the Nightingale
cluster, this page tells you how to access them.

The shared pool of computational nodes is called a batch queue. Jobs you
submit to it wait until there are resources available to run
them. Contact your PI to determine if your group has access to the batch 
queue on Nightingale and to find out what account you should use when 
submitting the batch jobs.

The computational cluster part of Nightingale is a shared pool of
individual computers within Nightingale called nodes that are available
for running your software. Because there are more than one compute node
on Nightingale, if your application can run on more than one computer at
a time, it can potentially run faster. Also, the batch system can run
your application as part of a "job", which is a block of instructions
that it will execute when there are compute nodes available to do the
work. That is, when you've submitted a job to be done, it will execute
the instructions in the job without you having to be logged into
Nightingale at all. You can queue up a bunch of jobs, each running a
useful calculation, and they will run sometime while you're away. This
makes the cluster very efficient at running software that can be broken
down into chunks that can each be done by a job. Jobs are typically
configured to write their results to a location on disk, and so you can
retrieve the results and read them when you log into Nightingale the
next time.

This page is meant to teach you how to put together a job on
Nightingale, submit it to the Nightingale job system, monitor the job
before it runs, during its run, after it's finished, and then how to
retrieve the results. Please see the example scripts page for scripts
that work on Nightingale that you can use and build from.

Nightingale Queues
##################

Users can view the partitions(queues) that they have the ability to submit batch jobs to, by typing the following command:
    [ng-login01 ~]$ sinfo -s -o "%.14R %.12l %.12L %.5D"
Users can also view specific configuration information about the compute nodes associated with their primary partition(s), by typing the following command:
    [ng-login01 ~]$ sinfo -p queue(partition)_name -N -o "%.8N %.4c %.16P %.9m %.12l %.12L %G"
    
The current limits in the Nightingale queues are below:
================  ==========  ==========  =======   ==============  ============
Queue(partition)	   CPUs       Memory     Max #        GPUs        Max Walltime
                  (per Node)	(per Node)   Nodes    Type : Count
                                                     (per node)
cpu	              64	        1TB	         16	      n/a	            7 days
a40	              64	        512GB	       2	      Tesla A40 : 1	  7 days
a100	            64	        256GB	       5	      Tesla A100 : 1	7 days
a100x2	          64	        512GB	       1	      Tesla A100 : 2	7 days
================  ==========  ==========  =======   ==============  ============


This page and the example scripts page assume that you have a working
knowledge of how to write and test a script, and you know at least
generally how jobs work. If you don't, but you want to run software on
compute nodes, the safest place to start is probably interactive jobs
(below). Please send us a ticket if you need help with this.

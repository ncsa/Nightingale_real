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



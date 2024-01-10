.. _faq:

Frequently Asked Questions
============================

Why does my login freeze when I'm trying to log into Nightingale?
----------------------------------------------------------------------

If you are trying to log in from outside the University of Illinois campus (not on the U of I network), you must be connected to either the University of Illinois VPN or the NCSA VPN; failing to connect through a VPN can cause your login to freeze (see :ref:`access_vpn`).

Why isn't my job running?
---------------------------

Slurm will block your job from starting if there is a reservation scheduled to start before your job would finish. 
If a reservation is blocking your job from starting, the ``squeue`` command will return a message like ``ReqNodeNotAvail, Reserved for maintenance`` for your job. 
You may be able to shorten the runtime of your job to fit in before the reservation starts. Refer to the :ref:`system-reservations` section for more details.

How should I acknowledge the use of Nightingale in my research?
------------------------------------------------------------------

Suggested acknowledgement text: "This research used resources of the National Center for Supercomputing Applications (NCSA) which is supported by funds from the University of Illinois Urbana-Champaign."

How do I get help if I can't find the answer in the documentation?
----------------------------------------------------------------------

If you can’t find the answer in the documentation (or via the search bar in the upper left corner) please :ref:`submit a support request <help>`. The ticket that is initiated will be used by NCSA staff to communicate with you to find a path to resoultion.

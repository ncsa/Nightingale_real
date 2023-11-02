.. _quick:

Quick Start Guide
==================

This information is for users who are adept at using an HPC system and are only interested in the basic Nightingale workflow.

- To access Nightingale, your project needs a *project group* set up with the resources that you need to use. The project's Principal Investigator (PI) sets up your project group. To begin the process of setting up access to Nightingale, the PI should fill out the NCSA Extensible Resource Allocation System (XRAS) form. Someone from the Nightingale project will contact you via email within a few days of filling out this form. See :ref:`access` for more details.

- Data stored on Nightingale may contain sensitive, regulated information. While Nightingale is set up to protect this data, users (you) are directly responsible for protecting it. Please read the full :ref:`protected` information before using Nightingale.

- You log into Nightingale using an Secure Shell (SSH) client on your local desktop or laptop. Because of the added security for Nightingale, you first log onto Nightingale’s secure node and then log onto a general access login node or, for groups that have them, a specialized interactive node. See :ref:`node_hostnames` for the node hostnames and step-by-step login instructions.

- See :ref:`queues` for the current limits of the Nightingale queues.

- Nightingale uses Slurm for job management. For information on how to submit batch jobs and interactive batch jobs, see :ref:`slurm`. :ref:`examples` are also available for reference.

- You will not work directly on your group’s curated project data in the /datasets directory. Instead, you will need to copy the data from the original directory to your home, scratch, or projects directory. Instructions on how to perform this data transfer can be found in :ref:`transfer`. If you ever need to transfer data **off of Nightingale**, read and follow the :ref:`protected` guidelines **before** transferring any data off of Nightingale.

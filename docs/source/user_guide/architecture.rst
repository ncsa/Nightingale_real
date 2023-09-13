=====================
System Architecture
=====================

Nightingale is a HIPAA-capable RedHat Linux OS High-Performance Computing (HPC) cluster 
designed to support UIUC researchers and collaborators who analyze 
sensitive, regulated data, like electronic Protected Health Information
(ePHI) or Controlled Unclassified Information (CUI). 
It provides standard batch computing options and interactive
compute nodes. 

The compute nodes are a mix of CPU and GPU (graphics processor unit) nodes. The GPU nodes are  
set up for double-precision (A100) or single-precision (A40) work.
The nodes are available as dedicated servers or shared
environments based on the needs of each research project. Nightingale
offers database services to support long-term data storage and
management with the ability to share and access relational databases on
the system. With 880 TB of high-speed parallel Lustre-based storage, the
system supports the researchers’ needs for sharing data and generating and storing results.

Interactive Login Nodes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- 2 interactive dual 64-core AMD **login** nodes each with 512GB RAM (*no GPUs*)


Interactive Group Nodes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- 3 interactive dual 32-core AMD **group** nodes each with 512GB RAM and 1 NVIDIA A40 GPU
- 2 interactive dual 32-core AMD **group** nodes each with 512GB RAM and 2 NVIDIA A100 GPUs
- 1 interactive dual 32-core AMD **group** node with 256GB RAM and 1 NVIDIA A100 GPU


Batch/Interactive Compute Nodes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- 16 batch/interactive dual 32-core AMD **compute** nodes each with 1TB RAM (*no GPUs*)
-  1 batch/interactive dual 32-core AMD **compute** node with 512GB RAM and 2 NVIDIA A100 GPUs
-  5 batch/interactive dual 32-core AMD **compute** nodes each with 256GB RAM and 1 NVIDIA A100 GPU
-  2 batch/interactive dual 32-core AMD **compute** nodes each with 512GB RAM and 1 NVIDIA A40 GPU

(NOTE: all batch nodes on Nightingale are diskless.  The OS and /tmp/ take up some of the RAM.  So user processes in batch jobs do not have every bit of physical RAM available while running.)

Storage
~~~~~~~~~~~~~~~~~~~~~~~~

-  880 TB of high-speed parallel Lustre-based storage
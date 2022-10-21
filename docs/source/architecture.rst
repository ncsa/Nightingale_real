=====================
System Architecture
=====================

Nightingale is a HIPAA-capable RedHat Linux OS High-Performance Computing (HPC) cluster 
designed to support UIUC researchers and collaborators who analyze 
sensitive, regulated data, like electronic Protected Health Information
(ePHI) or Controlled Unclassified Information (CUI). 
It provides standard batch computing options and interactive
compute nodes. The compute nodes are a mix of CPU and GPU nodes. The GPU nodes are  
set up for double precision (A100) or single precision (A40) work.
The nodes are available as dedicated servers or shared
environments based on the needs of each research project. Nightingale
offers database services to support long-term data storage and
management with the ability to share and access relational databases on
the system. With 880 TB of high-speed parallel LUSTRE-based storage, the
system supports the researchers’ needs for sharing data and generating and storing results.

Interactive Compute Nodes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  4 interactive compute/login nodes with dual 64-core AMDs and 512 GB
   of RAM
-  1 interactive node with 2 A100 GPUs, dual 32-core AMDs with 512GB RAM
-  1 interactive node with 1 A100 GPU, dual 32-core AMDs with 256GB RAM
-  5 interactive nodes with 1 A40 GPU, dual 32-core AMDs with 512GB RAM

Batch Compute System
~~~~~~~~~~~~~~~~~~~~~~~~

-  15 dual 64-core AMD systems with 1 TB of RAM
-  1 GPU compute node with 2 A100 GPUs, dual 32-core AMDs with 512GB RAM
-  4 GPU compute nodes with 1 A100 GPU, dual 32-core AMDs with 256GB RAM

Storage
~~~~~~~~~~~~~~~~~~~~~~~~

-  880 TB of high-speed parallel LUSTRE-based storage

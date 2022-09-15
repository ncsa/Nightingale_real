=====================
System Architecture
=====================

Introduction
-------------

Nightingale is a HIPAA-capable RedHat Linux OS High-Performance Computing (HPC) cluster 
designed to support UIUC researchers and collaborators who analyze 
regulated sensitive data, like electronic Protected Health Information
(ePHI) or Controlled Unclassified Information (CUI). It is located within the Advanced Computational Health Enclave
(ACHE), which is a special environment with restricted physical and
electronic access within NCSA’s National Petascale Computing Facility.
ACHE is a physically isolated 1000-square-foot data center that is
strictly managed following HIPAA standards along with NCSA and University of Illinois policies and
procedures to ensure conformance and protection of the stored data. The ACHE
undergoes annual security assessments and SOC 2 Type II certification.


Many of the restrictions that make the ACHE environment possible mean that some user tasks may be more complicated than other HPC systems. In particular, installing software may require interaction with Nightingale staff. These restrictions are described in the relevant areas of this documentation. 

Technical Specification
----------------------------

Nightingale provides standard batch computing options and interactive
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
-  6 interactive nodes with 1 A100 GPU, dual 32-core AMDs with 256GB RAM
-  5 interactive nodes with 1 A40 GPU, dual 32-core AMDs and 512GB RAM

Batch Compute System
~~~~~~~~~~~~~~~~~~~~~~~~

-  16 dual 64-core AMD systems with 1 TB of RAM
-  2 dual-A100 GPU compute nodes with 32-core AMDs and 512 GB of RAM

Storage
~~~~~~~~~~~~~~~~~~~~~~~~

-  880 TB of high-speed parallel LUSTRE-based storage

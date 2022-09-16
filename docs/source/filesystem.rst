###########
File System
###########

Nightingale uses a Lustre shared filesystem on all of its nodes. Lustre is an object-based, parallel distributed filesystem 
used for large-scale, high-performance computing clusters. It enables scaling to a large number of nodes (tens of thousands), 
petabytes (PB) of storage, and high aggregate throughput (hundreds of gigabytes per second). These features make Lustre an 
advantageous data storage solution for many scientific computing applications.

The table below describes the storage areas available on Nightingale's filesystem.

+--------------------+----------------+------------------------------------------+---------------------------------------------------+
| Purpose            | Location       | Quota Policy                             | Notes                                             |
+--------------------+----------------+------------------------------------------+---------------------------------------------------+
| datasets           | /datasets      | CSA-curated datasets, generally exported | Backup isn’t currently available on Nightingale,  | 
|                    |                | from Postgres. Read-only for the users.  | but will be added in the future and projects can  | 
|                    |                |                                          | use it for a fee.                                 |      
+--------------------+----------------+------------------------------------------+---------------------------------------------------+
| home               | /u             | 50GB                                     | Contains per-user home folders. Used for software,|
|                    |                |                                          | scripts, job files, etc. NOT intended as a        |
|                    |                |                                          | source/destination for I/O during jobs.           |
+--------------------+----------------+------------------------------------------+---------------------------------------------------+
| project            | /projects      | 1TB (more can be purchased)              | Contains per-group project folders. Used for      |
|                    |                |                                          | shared data for a project, common data sets,      |
|                    |                |                                          | software, results, etc.                           |
+--------------------+----------------+------------------------------------------+---------------------------------------------------+
| user scratch       | /scratch/users |                                          | Contains per-user scratch folders. Used by        |
|                    |                |                                          | running jobs for temporary storage during         |
|                    |                |                                          | computations.                                     |
+--------------------+----------------+------------------------------------------+---------------------------------------------------+
| local scratch      | /tmp           |                                          | On compute nodes it is private to a running Slurm |
|                    |                |                                          | job. It is purged when the job completes.         |
|                    |                |                                          |                                                   |
+--------------------+----------------+------------------------------------------+---------------------------------------------------+  
 
**Home**

The /home area of the file system is where users land upon logging in to the cluster via SSH, and is where a user’s $HOME env. variable points. This is meant to contain a user’s configuration files, job output/error files, and smaller software installations. A user’s /home area of the file system is automatically created during the account provisioning process.

**Project**

The /projects area of the file system is where a group’s (be they a single faculty member, a lab group, a department, or an entire college) storage capacity resides. Users can have access to multiple project subdirectories if they are a member of various groups, and have been granted access to the space by the PI.

**User Scratch**

The /scratch area of the file system is where users can place data while it is under active work.

**Scratch — Local**

The /tmp area is a local file system on an individual compute node, it is not part of the shared file system. Data place in /tmp is purged following a job’s completion prior to the next job beginning on the node.

 




 



 





  

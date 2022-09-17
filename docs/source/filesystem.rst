###########
Filesystem
###########

Nightingale uses a Lustre shared filesystem on all of its nodes. Lustre is an object-based, parallel distributed filesystem 
used for large-scale, high-performance computing clusters. It enables scaling to a large number of nodes (tens of thousands), 
petabytes (PB) of storage, and high aggregate throughput (hundreds of gigabytes per second). These features make Lustre an 
advantageous data storage solution for many scientific computing applications.

The table below describes the storage areas available on Nightingale's filesystem.

.. table:: Nightingale Storage Areas
   :align: "left"

=============== ================ =================================== 
Location        Purpose          Quota Policy                        
=============== ================ =================================== 
 /u              home            50GB                               
 /projects       projects        | 1TB (more can be purchased)                    
 /scratch/users  user scratch    |                                    
 /tmp            local scratch   |                
 /datasets       datasets        |   
=============== ================ ===================================                                                                 
                                                                 
The following sections give specific information on the purpose of these areas.
 
**Home**

The /u area of the filesystem is where users land upon logging on to the cluster via SSH, and is where a user’s $HOME environment variable points. This area has a fairly small quota and is meant to contain a user’s configuration files, job output/error files, and smaller software installations. This area is automatically set up during the account provisioning process. It is not possible to request an expansion of home directory quota. If a user depletes the available space on their home directory, they will be notified and and given the opportunity to remove files from it. At some point the data will be cleared to get below the 50GB threshold.

**Project**

The /projects area of the filesystem is where members of a group (be they a single faculty member, a lab group, a department, or an entire college) store their project-related files. A user can have access to multiple project subdirectories if they are a member of various groups, and have been granted access to the space by the project's Principal Investigator (PI).

**User Scratch**

The /scratch area of the filesystem is where users can place data temporarily while it is being used by a running job.

**Local Scratch**

The /tmp area is a local filesystem on an individual compute node and is not part of the shared file system. Data placed in /tmp is purged when the job completes.

**Datasets**
 
The /dataset area contains curated datasets typically exported from Postres. This data is read only.




 



 





  

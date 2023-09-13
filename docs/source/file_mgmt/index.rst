File Management
=================

Nightingale Filesystem
-------------------------

Nightingale uses a Lustre shared filesystem on all of its nodes. Lustre is an object-based, parallel distributed filesystem for large-scale, high-performance computing clusters. It enables scaling to a large number of nodes (tens of thousands), petabytes (PB) of storage, and high aggregate throughput (hundreds of gigabytes per second). These features make Lustre an advantageous data storage solution for many scientific computing applications.

The table below describes the location, purpose, and quota policy for the storage areas available on Nightingale's filesystem.

.. list-table:: Nightingale Storage Areas
   :widths: 15 15 35
   :header-rows: 1

   * - Location
     - Purpose
     - Quota Policy
   * -  /u
     - home
     - 50GB
   * - /projects       
     - projects
     - 1TB (more can be purchased)                    
   * - /scratch/users  
     - user scratch
     - 
   * - /tmp 
     - local scratch
     - 
   * - /datasets
     - datasets
     - 
                                                                 
More information about these storage areas is described in the following sections.
 
**Home**

The /u area of the filesystem is where users land upon logging on to the cluster  and is where a user’s $HOME environment variable points. This area has a fairly small quota and is meant to contain a user’s configuration files, job output/error files, and smaller software installations. This area is automatically set up during the account provisioning process and there is no additional charge for this storage. It is not possible to request an expansion of the home directory quota. If a user depletes the available space on their home directory, they will be notified and given the opportunity to remove files from it. You will need to delete files to get below the threshold and will not be able to store additional data.

**Project**

The /projects area of the filesystem is where group members (be they a single faculty member, a lab group, a department, or an entire college) store their project-related files. A user can have access to multiple project subdirectories if they are a member of multiple groups and have been granted access to the space by the project's Principal Investigator (PI). Projects pay a separate charge for this project space and the minimum allocation is 1 TB. Additional space can be purchased as needed.

**User Scratch**

The /scratch area of the filesystem is where users can place data temporarily while a running job is using it.

**Local Scratch**

The /tmp area is a local filesystem on an individual compute node and is not part of the shared file system. Data placed in /tmp is purged when the job completes.

**Datasets**
 
The /dataset area contains curated, read-only datasets typically exported from a Postgres database. Projects will be informed when data is placed here for them.

Transferring Files
-------------------

Copying project data to your home directory
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You will not work directly on your group's curated project data in the /datasets directory. Instead, you will need to copy the data from the original directory to your home directory.  Follow the steps below.

Enter the **cd** command to go your home directory::

   cd 

Using the **mkdir** command, create a new folder in your home directory using a name of your choosing::

   mkdir <folder_name>

Using the **cp** command, copy the dataset to the folder you created. (cp -R command is used for recursive copy of all files and directories in the source directory tree.)::

   cp -R /<dataset_foldername>/<filename> ~/<your_data_folder_name>
   
For example, if the dataset you want is located in '/datasets/covid_1' and you want to move it to your directory 'my_covid_data,' you would enter the command::

   cp -R /datasets/covid_1 ~/my_covid_data

To check if you copied the data successfully, enter the commands::

   cd ~/my_covid_data/covid_1
   ls

Copying Files On To Nightingale Using SCP
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

SCP (Secure Copy) is an application that gives users a secure way to copy files between machines over an unsecured network. Its syntax is similar to that of SSH used to log into a remote machine.

SCP requires a source and a destination. You can use it to copy individual files or directories. The source and destination are specified with a file path (if it is on your local machine) and as <login_name>@<machine_name>:<file_name> (if it is on a remote machine).

Since Nightingale has a bastion host which all network traffic travels through, you need to specify that the copy will jump through the bastion. For example, if user "test1" is copying file "my_data" from their current directory on their local machine to their home directory on the Nightingale login node "ng-login01" they would use the following command::

   scp -J test1@ngale-bastion-1.ncsa.illinois.edu my_data test1@ng-login01:.
   
Copying Files On To Nightingale Using AWS S3 Buckets
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In order to use AWS S3 Buckets you must first configure the service. Run the command “aws configure” and answer its prompts for the following data:

* AWS Access Key ID
* AWS Secret Access Key
* Default region name
* Default output format

Copy files from the bucket using::

Copying Files Off of Nightingale
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Any method that can transfer data to Nightingale can also be used to transfer information off of the machine. 

However, before doing so please read about `protected data <../protected_data.rst>`_.
Data transfers off of Nightingale are audited and must be accounted for.



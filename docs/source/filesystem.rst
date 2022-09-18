###############
File Management
###############

Nightingale Filesystem
======================

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

Creating and Editing Files
==========================

Sometimes it is easiest to create and edit your files directly on the cluster rather than transfer them back and forth. A variety of programs are available on clusters that you can use for working with plain text files. Examples include vi/vim, gedit, nano, and emacs. The vi/vim text editor is one of the most commonly used. However, if you are new to working in the Linux environment the nano editor is recommended because it may be more similar to the way you edit text files on a non-Linux based machine. 

GNU nano
--------

GNU nano is an easy to use command line text editor for Linux. To open an existing file or to create a new file, type nano followed by the file name.

nano file_name

This opens a new editor window in your terminal where you can start editing the file.  At the bottom of the window, you will find a list of shortcuts to use with the nano editor.  The caret symbol (^) represents the Ctrl key (e.g. to exit type Ctrl+X). The letter M represents the Alt key (e.g. to undo type Alt+U).

MobaTextEditor
--------------

If you use MobaXterm to log into Nightingale, you will see a file browser in the left pane of the MobaXterm window.  Double-click on a selected file to open it in a separate window.  Please note that a temporary copy of files will be saved on your local machine when you use MobaTextEditor.  The temporary files are saved in the AppData\Roaming folder on Windows and will be removed when you fully close MobaXterm on your machine.

Transferring Files
==================

Coping data to your home directory
To work on the files, you will need to copy the data from the original directory to your home directory.  Follow the steps below.

Go to your home directory:

cd 

Create a new folder in your home directory called shield_data_folder (you can pick a different name):

mkdir shield_data_folder

Copy the croc_req_1 folder with the data to your new folder:

cp -R /datasets/croc_req_1 ~/shield_data_folder

Check if you copied the data successfully:

cd ~/shield_data_folder/croc_req_1
ls


File Organization
=================

How you organize your files depends somewhat on how the directory structure is set up on your cluster and possibly guidelines set up by your project manager. However, there are some basic goals you should keep in mind.

- File names should be logical so that you can find them a week from now, a month from now, and a year from now. Data that cannot be found later is not worth nearly    as much as data you can quickly locate. When storing your files to an archive, organize them with this goal in mind so they are stored logically and can be accessed easily. 
 
- Use Tar, Winzip, or similar file-bundling software to create a single file from a directory tree, and then store that file. The name of that bundled file should clearly indicate what files are bundled within.
 
- Apply meaningful names to files and directories in an archival storage site so that you, or your colleagues, can navigate back to data that you need when you need it. It is up to you to decide what works best.


 



 





  

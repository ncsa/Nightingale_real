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

File Transfers with Globus
-----------------------------

.. warning::

   As of January 2023, Globus is now available for use on Nightingale.  However, we have not finished the final contracts and setup for specifically HIPAA-data certified variant of globus, so do not transfer HIPAA data over globus at this time.  When HIPAA-certified Globus is installed, this warning will be removed.  If you have any questions about data movement, please don't hesitate to put in a ticket (:ref:`help`).  

Globus is a web-based file transfer system that works in the background to move files between systems with "Globus Endpoints".  Nightingale will have a permanent Globus Endpoint (with a name announced at that time).  To transfer files to and from your directories using Globus, you will have to authenticate that endpoint, using your already-existing NCSA username, password, and NCSA account on Duo. 

One-time Setup
~~~~~~~~~~~~~~~~

You will need to set up a separate account on globus.org, that will have a username and a separate password.  To use Globus to transfer files to and from Nightingale, you will need to "link" your new Globus account with your NCSA identity.  Log into globus.org, click on "Account" in the left sidebar, then click on the "Identities" tab.  If your NCSA username and email address is not in that list, then click "Link Another Identity" in the upper right to link it.

Using Globus to Transfer Files
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Once your identity is linked (above) then do the following to transfer files using Globus.

Navigate to globus.org and click “Log In” in the upper right corner

We recommend you use an independent password for your globus account.  If you're doing that, on the "Log in to use Globus Web App" screen, click on "Globus ID to sign in" at the very bottom, and sign in with your globus password.  

If prompted click “Allow” when asked to authorized the Globus Web App

.. image:: images/file_mgmt/Screen-Shot-2021-01-19-at-9.22.30-PM-768x506.png

Once logged in you should be taken to the File Manager section, on one side search for "ngale" and click on the "ncsa#ngale" endpoint from the resulting list:

.. image:: images/file_mgmt/ngale_globus_ngale_endpoint.png

The system will prompt you to Authenticate to the endpoint, click continue; Globus may prompt you to link your netid@illinois.edu identity, go ahead and do so.  You will need provide your NCSA Duo authority here.  

.. image:: images/file_mgmt/Screen-Shot-2021-01-19-at-9.23.26-PM-768x299.png

.. image:: images/file_mgmt/Screen-Shot-2021-01-19-at-9.51.47-PM-768x280.png

.. image:: images/file_mgmt/Screen-Shot-2021-01-19-at-9.52.00-PM-768x657.png

You should then get dropped back into the “File Manger” view.  You can navigate from there to your home directory (under "/u") or to your project directory under /projects.  

.. image:: images/file_mgmt/ng_globus_system_dir.png

Then in a similar manner (in the right half of the “File Manger” view) search for and authenticate to the collection you are planning to transfer data to/from, then use the GUI to transfer the data; you can choose transfer settings. Also on the left is a button to view your current transfer activity

.. image:: images/file_mgmt/Screen-Shot-2021-01-19-at-9.39.22-PM-1024x141.png

Creating and Editing Files
---------------------------

Sometimes, it is easiest to create and edit your files directly on the cluster rather than transfer them back and forth. 
You can use various programs on clusters for working with plain text files. Examples include vi/vim, gedit, nano, and emacs. 
The vi/vim text editor is one of the most commonly used. However, if you are new to working in the Linux environment, 
the nano editor is recommended because it may be more similar to how you edit text files on a non-Linux-based machine. 
Several tutorials are available online if you want to know more about nano or vi. A couple of suggestions are listed below.

- `How-to-Geek: The Beginner’s Guide to Nano, the Linux Command-Line Text Editor <https://www.howtogeek.com/howto/42980/the-beginners-guide-to-nano-the-linux-command-line-text-editor/>`_

- `Wikibooks: Learning the vi Editor <https://upload.wikimedia.org/wikipedia/commons/d/d2/Learning_the_vi_Editor.pdf>`_ 

You can also edit files using MobaXterm's text editor. Brief instructions for using GNU nano and MobaXterm are given below.

GNU nano
~~~~~~~~~

GNU nano is an easy-to-use command line text editor for Linux. To open an existing file or create a new one, type nano followed by the file name::

   nano file_name

This opens a new editor window in your terminal where you can start editing the file. At the bottom of the window, you will find a list of 
shortcuts to use with the nano editor. The caret symbol (^) represents the Ctrl key (e.g., to exit, Nano shows ^X, type Ctrl+X). The letter M represents the 
Alt key (e.g., Nano shows M-U, to undo type Alt+U).

MobaTextEditor
~~~~~~~~~~~~~~~

If you use MobaXterm to log into Nightingale, you will see a file browser in the left pane of the MobaXterm window.  Double-click on a selected 
file to open it in a separate window.  Please note that a temporary copy of files will be saved on your local machine when you use MobaTextEditor.  
The temporary files are saved in the AppData\Roaming folder on Windows and will be removed when you fully close MobaXterm on your machine.

Organizing Files
------------------

How you organize your files depends somewhat on how the directory structure is set up on your cluster and possibly guidelines set up by your project 
manager. However, there are some basic goals you should keep in mind.

- File names should be logical so that you can find them a week from now, a month from now, and a year from now. Data that cannot be found later is not worth nearly as much as data you can quickly locate. When storing your files to an archive, organize them with this goal in mind so they are stored logically and can be accessed easily. 
 
- Use Tar, Winzip, or similar file-bundling software to create a single file from a directory tree, and then store that file. The name of that bundled file should clearly indicate what files are bundled within.
 
- In an archival storage site, apply meaningful names to files and directories so you or your colleagues can navigate back to the data when needed. 
It is up to you to decide what works best.


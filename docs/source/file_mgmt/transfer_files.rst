##################
Transferring Files
##################

Copying project data to your home directory
===========================================

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
=========================================
SCP (Secure Copy) is an application that gives users a secure way to copy files between machines over an unsecured network. Its syntax is similar to that of SSH used to log into a remote machine.

SCP requires a source and a destination. You can use it to copy individual files or directories. The source and destination are specified with a file path (if it is on your local machine) and as <login_name>@<machine_name>:<file_name> (if it is on a remote machine).

Since Nightingale has a bastion host which all network traffic travels through, you need to specify that the copy will jump through the bastion. For example, if user "test1" is copying file "my_data" from their current directory on their local machine to their home directory on the Nightingale login node "ng-login01" they would use the following command::

   scp -J test1@ngale-bastion-1.ncsa.illinois.edu my_data test1@ng-login01:.
   
Copying Files On To Nightingale Using AWS S3 Buckets
====================================================

In order to use AWS S3 Buckets you must first configure the service. Run the command “aws configure” and answer its prompts for the following data:

* AWS Access Key ID
* AWS Secret Access Key
* Default region name
* Default output format

Copy files from the bucket using::

Copying Files Off of Nightingale
=========================================

Any method that can transfer data to Nightingale can also be used to transfer information off of the machine. 

However, before doing so please read about :ref:`Protected Data`.

Data transfers off of Nightingale are audited and must be accounted for.

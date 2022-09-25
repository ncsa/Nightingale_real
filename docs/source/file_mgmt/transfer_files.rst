##################
Transferring Files
##################

Copying project data to your home directory
===========================================

You will not work directly on your group's curated project data. Rather to work with them, you will need to copy the data from the original directory to your home directory.  Follow the steps below.

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

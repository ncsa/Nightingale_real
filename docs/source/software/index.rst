Software
==========

.. note::
   You are allowed to install software in spaces you have access to (home, project)
   When installing any software you should consider the following:

   - Home directory disk usage quotas.
   - Will the software be used by multiple users in my group?
     (Project space is the **recommended** location to install software.)
   - Does the desired software have dependencies/requirements?
   - Is the prerequisite software already installed?
 
Installed Software
-------------------

The table below shows the core software and libraries available on Nightingale. You can use `module commands <modules>`_ to add this software to your
software environment.

===========        ========================
Software           Version
===========        ========================
Anaconda           2022.05  (python 3.9.12)
awscli             2.4.16
Cuda               11.4.2
GCC                12.2.0
Julia              4.3.2
MATLAB             9.7
Miniconda          2022.05  (python 3.9.12)
R                  4.2.0
===========        ========================

Using Modules
--------------

Nightingale uses `Environment Modules <https://modules.readthedocs.io/en/stable/index.html>`_, a set of module commands that 
enable users to dynamically configure their software environment. Essentially, you can turn access to 
software on or off by "loading" or "unloading" a modulefile that adds or removes the software's configuration in your user 
environment. The table below shows the most common module commands you will need on Nightingale.

+--------------------+-------------------------------------------------+
| Command            | Description                                     |
+--------------------+-------------------------------------------------+
| module avail       | Lists the modules that are available. If you    |
|                    | are looking for a piece of software but typing  |
|                    |                                                 |
|                    | the command to run it gets you a "command not   |
|                    | found" error, then loading the modulefile for   |
|                    |                                                 |
|                    | that specific piece of software first is        |
|                    | probably what you need to do.                   |
+--------------------+-------------------------------------------------+
| module list        | Lists the modules that you currently have       |
|                    | loaded in your current user environment.        |
+--------------------+-------------------------------------------------+
| module help        | Provide general information on what the         |
| *modulefile*       | modulefile does to your current user            |
|                    | environment when loaded.                        |
+--------------------+-------------------------------------------------+
| module display     |                                                 |
| *modulefile*       |                                                 |
|                    | Display (or show) the changes that loading the  |
| or                 | modulefile will make to the user environment.   |
|                    |                                                 |
| module show        |                                                 |
| *modulefile*       |                                                 |
+--------------------+-------------------------------------------------+
| module load        | Loads a modulefile [or modulefiles] into your   |
| *modulefile (      | current shell environment (see "module avail"   |
| modulefile2 ...)   |                                                 |
|                    | above to get a list)                            |
|                    |                                                 |
+--------------------+-------------------------------------------------+
| module unload      | Unloads a modulefile; if you unload a           |
| *modulefile*       | modulefile you had previously loaded, then the  |
|                    |                                                 |
|                    | software is no longer available to you (in your |
|                    | current shell environment).                     |
+--------------------+-------------------------------------------------+
| module swap        | Unloads one *modulefile1* and loads another     |
| oldmod             | *modulefile2*. This is typically used to change |
| newmod             |                                                 |
|                    | the version of a modulefile that you have       |
|                    | loaded.                                         |
+--------------------+-------------------------------------------------+
| module save        | If you have modulefiles that you want to load   |
|                    | every time you log in, then you can set up your |
|                    |                                                 |
|                    | account so that they are loaded every time you  |
|                    | log in without you having to type the "module   |
|                    |                                                 |
|                    | load" every time. Do this by first loading the  |
|                    | modulefiles you always want to have loaded.     |
|                    |                                                 |
|                    | Then type "module save". The system will save   |
|                    | your current module list as your default. When  |
|                    |                                                 |
|                    | you log in the next time, these modulesfiles    |
|                    | will already be loaded.                         |
+--------------------+-------------------------------------------------+

These commands will enable you to get started using modules. If you are curious about the additional capabilities of the module command, see the `Environment Modules Documentation <https://modules.readthedocs.io/en/stable/index.html>`_.

**Notes:** 

- Modules are independent of which shell is being used. Therefore, the module commands are the same for all shells (bash, tcsh, ksh, etc.). 
- The order in which module commands are issued is important because the changes are prepended to the current user environment paths with each module load.

Using Python on Nightingale
-----------------------------

Introduction
~~~~~~~~~~~~~~~

Python is an interpreted, high-level, general-purpose programming language. Python and Python packages are available via the `Python Package Index (PyPI) <https://pypi.org/>`_ , which hosts thousands of third-party modules for Python. Both Python’s standard library and the community-contributed modules allow for endless possibilities. Anaconda also provides a Python environment with python packages.


Anaconda is a free, open-source distribution of the Python and R programming languages. 
Anaconda (ver 2022.05) and Miniconda (ver 2022.05) are installed on
Nightingale. One of the main differences between Anaconda
and Minconda is the number of packages: Anaconda by default installs
with over 150 data science packages, whereas Miniconda by default
installs a subset of the packages installed by default with Anaconda. 
Anaconda includes Conda, which is a package manager and environment 
management system. It is a popular package manager for Python and R. 


Versions
~~~~~~~~~

The table below lists the versions of Python installed on the Nightingale.
     
.. list-table:: 

   * - Anaconda 2022.05
     - Python 3.9.12
   * - Miniconda 2022.05
     - Python 3.9.5

Adding Python To Your Environment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Each Python installation on Nightingale has a corresponding modulefile for loading a specific version of 
Python into your software environment. To see the available Python versions type the following on the command line::

   module avail anaconda3

or::

   module avail miniconda3

See `Using Modules <modules>`_ for more information about modules.

Installing Python Packages (in user specified locations)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
 
You must install software/libraries into user-writeable locations like your home directory, your group’s project space, or your scratch space. Software installed in scratch space is not permanent, and system administrators may remove it at any time. We recommend that you install it in your group’s project space instead.

Generally, any Python package not available in the system installation can be 
installed from the `Python Package Index <https://pypi.org/>`_ (PyPI)  in your specified location.

The following commands will create a minimal clone anaconda environment in your home directory, install pytorch, and list the Python packages 
installed (including your own installed packages) in your environment::

  cd ${HOME}
  module load anaconda3/2022.05
  export CONDA_PKGS_DIRS="${HOME}/.conda/pkgs"
  conda create -n my.anaconda python
  conda info -e
  source activate my.anaconda
  conda info -e
  conda install pytorch
  conda list
 
To deactivate the anaconda environment type::

  conda deactivate

To create a complete clone anaconda environment replace::

  conda create -n my.anaconda python
 
with::

  conda create -n my.anaconda anaconda

Viewing Installed Python Packages
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

After enabling Python in your user environment by loading a Python or Anaconda modulefile, you can view a list of the Python packages 
installed (including your own installed packages) by typing the following commands.

If you have loaded a Python modulfile, type::

   pip list

if you have loaded an Anaconda modulefile, type::

   conda list

Using R on Nightingale
-----------------------

Introduction
~~~~~~~~~~~~~~

R is a programming language and software environment for statistical computing and graphics. It is an interpreted language typically accessed through a command-line interpreter. R and its libraries implement a wide variety of statistical and graphical techniques, such as linear and non-linear modeling, classical statistical tests, time-series analysis, classification, and clustering.

R is easily extensible through functions and extensions. The R community is noted for its active contributions to developing R packages. R packages contain code, data, and documentation in a standardized collection format that R users can install. R and R packages are available via the `Comprehensive R Archive Network (CRAN) <https://cran.r-project.org>`_, a collection of sites that carry identical material, consisting of the R distribution(s), the contributed extensions, documentation for R, and binaries.

Versions
~~~~~~~~~

The table below lists the versions of R currently installed on Nightingale.

+---------+
| Version |
+---------+
| R 4.2.0 |
+---------+

Adding R to Your Environment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You can use a module file to load a specific R version into your user environment.::

   module avail R

The latest version of R available on the Nightingale can be loaded into your environment by typing::

   module load R

To load a specific version, you will need to load the corresponding module. (See `Using Modules <modules>`_ for more information about modules.)

Installing Add-on Packages
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Any R add-on package not available in the system installation can be installed from the CRAN in a user-specified location. 
You must have write access to the location.

Installation Command Syntax
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~`

R package installations are generally straightforward. Minimally, all that is needed is the package's name. You can also specify additional information, such as installation location and the repository.
 
The syntax for the install R packages command is::

   install.packages()
 
Two example installations specifying “Package Name”, “Location”, and “Repository” and the resulting behavior are shown below.

**Example 1**::

   install.packages('package_name', '/path/to/r_libraries', 'Repository URL')
   
Installs the package downloaded from the specified repository in the specified location

**Example 2**::

  install.packages('package_name.tar.gz', '/path/to/r_libraries', repos = NULL)

Installs the local package(file) in the specified location specifying no repository(NULL)

When the installation location and the repository URL are not specified, R packages are installed in a default location, and the R installation process prompts you to choose from a list of repositories. R packages downloaded manually from the CRAN can be installed by specifying the local filename and omitting the repository URL (specifying NULL).

Using Rscript
~~~~~~~~~~~~~~

You can use the rscript command to run R commands without starting an R session. As a scripting front end for R, Rscript enables using R via shell scripts and scripting applications.

The examples below show step-by-step the commands you can run on Nightingale. In these steps, ~/Rlibs is used for the location to install user-specific add-on packages (The tilde "~" means the users' home directory—i.e. $HOME).

**Note:** These examples use the BASH shell. The command syntax may differ when using a different shell.

**Step 1:** Set the HTTPS_PROXY environment variable (if you have not already done so)::

  export HTTPS_PROXY=http://ache-proxy.ncsa.illinois.edu:3128

**Step 2:** Create a directory for your R packages::

   mkdir ~/Rlibs

**Step 3:** Load the R modulefile::
 
   module load R/4.2.0

**Step 4:** Set the R library environment variable (R_LIBS) to include your R package directory::

  export R_LIBS=~/Rlibs:$R_LIBS

**Step 5:** Use the install.packages command to install your R package::

  Rscript -e "install.packages('RCurl', '~/Rlibs', 'https://cran.r-project.org')"

If the environment variable R_LIBS is not set, and a directory is not specified with the install.packages command, then R packages will be installed under ~/R/x86_64-unknown-linux-gnu-library by default. (This R subdirectory structure is created automatically.) The R_LIBS environment variable will need to be set every time when logging in to the Nightingale if your R package location is to be visible to an R session. You can add the following code to your ~/.bashrc file to remove the need to set the R_LIBS environment variable with every login session to the Nightingale.::

   if [ -n $R_LIBS ]; then
         export R_LIBS=~/Rlibs:$R_LIBS
   else
         export R_LIBS=~/Rlibs
   fi
 
Warnings and Error Messages
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

R packages that are not available in the current CRAN (Comprehensive R Archive Network) or if the name of the package is misspelled tend to generate a message 
similar to the following::

   [ng-login01 ~]$ Rscript -e "install.packages('phybase','~/Rlibs', 'http://ftp.ussg.iu.edu/CRAN')"
   Warning message:
   package 'phybase' is not available (for R version 3.2.2)
 
Searching the CRAN site for your desired R package may provide links to archived versions that are not available in the current CRAN. In this case, the specific 
archived R package can be downloaded and installed from the local file using the same command but omitting the repository URL (specifying NULL).
Some R packages have dependencies and require them to be installed first and will generate an error message similar to the following::

   [ng-login01 ~]$ Rscript -e "install.packages('phybase_1.1.tar.gz', '~/Rlibs',  repos = NULL)"
   ERROR: dependency 'ape' is not available for package 'phybase'
   * removing '/home/jdoe/Rlibs/phybase'
   Warning message:
   In install.packages("phybase_1.1.tar.gz", repos = NULL) :
     installation of package 'phybase_1.1.tar.gz' had non-zero exit status
 
Installing the required R package first and then the desired R package resolves this issue.

Viewing Installed R Packages
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You can use the library() command to view all user and system-installed R packages (user-installed packages are only visible to R when the $R_LIBS environment variable is set)::

   [ng-login01 ~]$ Rscript -e "library()"

   Packages in library '/home/jdoe/Rlibs':

   R6                      Classes with reference semantics
   RCurl                   General network (HTTP/FTP/...) client interface
                           for R
   ...
   stringr                 Simple, Consistent Wrappers for Common String
                           Operations
   whisker                 {{mustache}} for R, logicless templating


   Packages in library '/sw/apps/R/R-4.2.0/lib64/R/library':

   KernSmooth              Functions for kernel smoothing for Wand & Jones
                           (1995)
   MASS                    Support Functions and Datasets for Venables and
                           Ripley's MASS
   ...
   tools                   Tools for Package Development
   utils                   The R Utils Package


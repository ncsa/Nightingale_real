Software
==========

You can install software in spaces you have write-access to (home, projects, scratch). Project space is the **recommended** location to install software. Consider the following when installing any software:

- Home directory disk usage quotas.
- Will the software be used by multiple users in my group?
- Does the desired software have dependencies/requirements?
- Is the prerequisite software installed?

.. _installed:

Installed Software
-------------------

The table below shows the core software and libraries available on Nightingale. 
You can use module commands (see :ref:`modules`) to add this software to your software environment.

==============================================================================   ========================
Software                                                                         Version
==============================================================================   ========================
Anaconda_                                                                        2022.05  (Python 3.9.12)
`awscli <https://aws.amazon.com/cli/>`_                                          2.4.16
`Cuda <https://docs.nvidia.com/cuda/archive/11.4.2/>`_                           11.4.2
`GCC <https://gcc.gnu.org/onlinedocs/12.2.0/>`_                                  12.2.0
`Julia <https://juliahub.com/ui/Packages/General/RegistryCI/4.3.2>`_             4.3.2
`MATLAB <https://www.mathworks.com/help/?s_tid=gn_supp>`_                        9.7
`Miniconda <https://docs.conda.io/projects/miniconda/en/latest/index.html>`_     2022.05  (Python 3.9.12)
`R <https://cran.r-project.org/bin/windows/base/old/4.2.0/NEWS.R-4.2.0.html>`_   4.2.0
==============================================================================   ========================
 
.. _Anaconda: https://docs.anaconda.com/free/anaconda/reference/release-notes/#anaconda-2022-05-may-10-2022



.. _modules:

Using Modules
--------------

Nightingale uses `Environment Modules <https://modules.readthedocs.io/en/stable/index.html>`_. 
Turn access to software on or off by **loading** or **unloading** a modulefile; this adds or removes the software's configuration in your user environment. 
The table below shows the most common module commands you will use on Nightingale.

.. note::
   
   - Module commands are the same for all shells (Bash, tcsh, ksh, and others). 
   - The order that module commands are executed in is important. Changes are *prepended* to the current user environment paths with each module load.
   - In the module commands below, replace **modulefile**, **modulefile2**, **oldmod**, and **newmod** with the names of the modulefile(s) you are running the command on.

+--------------------+-------------------------------------------------------------------------------+
| Command            | Description                                                                   |
+====================+===============================================================================+
| ``module avail``   | Lists the modules that are *available*.                                       |
+--------------------+-------------------------------------------------------------------------------+
| ``module list``    | Lists the modules that are *loaded* in your user environment.                 |
+--------------------+-------------------------------------------------------------------------------+
| ``module help      | Provides general information on what the modulefile does to your current user |
| modulefile``       |                                                                               |
|                    | environment, when loaded.                                                     |
+--------------------+-------------------------------------------------------------------------------+
| ``module display   | Displays (or shows) the changes that loading the modulefile will make to your |
| modulefile``       |                                                                               |
|                    | current user environment.                                                     |
| or                 |                                                                               |
|                    |                                                                               |
| ``module show      |                                                                               |
| modulefile``       |                                                                               |
+--------------------+-------------------------------------------------------------------------------+
| ``module load      | Loads a modulefile(s) into your current shell environment.                    |
| modulefile (       |                                                                               |
| modulefile2 ...)`` |                                                                               |
+--------------------+-------------------------------------------------------------------------------+
| ``module unload    | Unloads a modulefile. If you unload a modulefile you had previously loaded,   |
| modulefile``       |                                                                               |
|                    | then the software is no longer available in your current shell environment.   |
+--------------------+-------------------------------------------------------------------------------+
| ``module swap      | Unloads the oldmod and loads the newmod. This is typically used to change the |
| oldmod newmod``    |                                                                               |
|                    | version of a modulefile that you have loaded.                                 | 
+--------------------+-------------------------------------------------------------------------------+
| ``module save``    | If you have modulefiles that you want to load every time you log in, without  |
|                    |                                                                               |
|                    | having to use the ``module load`` command each time:                          |
|                    |                                                                               |
|                    | #. Load the modulefiles you always want to have loaded.                       |
|                    |                                                                               |
|                    | #. Type ``module save``. When you log in next time, these modulefiles will    |
|                    |                                                                               |
|                    | already be loaded.                                                            |
+--------------------+-------------------------------------------------------------------------------+

For more information on module commands, see the `Environment Modules Documentation <https://modules.readthedocs.io/en/stable/index.html>`_.

Using Python on Nightingale
-----------------------------

Introduction
~~~~~~~~~~~~~~~

`Python <https://en.wikipedia.org/wiki/Python_(programming_language)>`_ is a general-purpose programming language. Python and Python packages are available via `Python Package Index (PyPI) <https://pypi.org/>`_, which hosts thousands of third-party modules for Python. Both Python’s standard library and the community-contributed modules allow for endless possibilities. 

Anaconda and Miniconda also provide a Python environment with Python packages.
Anaconda and Miniconda are installed on Nightingale. 
One of the main differences between Anaconda and Miniconda is the number of default packages: 

- Anaconda, by default, installs with over 150 data science packages. 
- Miniconda, by default, installs with a subset of the packages installed with Anaconda. 

Anaconda and Miniconda include `Conda <https://docs.conda.io/en/latest/>`_, which is a package manager and environment management system popular for Python and R. More information on whether Anaconda or Miniconda is best for your needs is available in the `Anaconda documentation <https://docs.anaconda.com/free/anaconda/getting-started/distro-or-miniconda.html>`_

Versions
~~~~~~~~~

See :ref:`installed` for the versions of Anaconda, Miniconda, and Python installed on Nightingale.

Adding Python to Your Environment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Each Python installation on Nightingale has a corresponding modulefile for loading a specific version of Python into your software environment. 
To see the available Python versions type the following in the command line:

.. code-block::

   module avail anaconda3

or

.. code-block::

   module avail miniconda3

Installing Python Packages (in User-Specified Locations)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
 
You must install software/libraries in spaces you have write-access to (user-writeable) like your home directory, your group’s project space (**recommended**), or your scratch space. Software installed in scratch space is **not permanent** and system administrators may remove it at **any time**. 

Generally, any Python package not available in the system installation can be installed from the `PyPI <https://pypi.org/>`_ in your specified location.

The following commands will create a minimal clone anaconda environment in your home directory, install `PyTorch <https://pytorch.org/docs/stable/index.html>`_, and list the Python packages installed in your environment (including your own installed packages):

.. code-block::

  cd ${HOME}
  module load anaconda3/2022.05
  export CONDA_PKGS_DIRS="${HOME}/.conda/pkgs"
  conda create -n my.anaconda python
  conda info -e
  source activate my.anaconda
  conda info -e
  conda install pytorch
  conda list
 
To create a complete clone anaconda environment, 

   replace:

   .. code-block::

      conda create -n my.anaconda python
 
   with:

   .. code-block::

      conda create -n my.anaconda anaconda

To deactivate the anaconda environment:

.. code-block::

   conda deactivate

Viewing Installed Python Packages
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

After enabling Python in your user environment (by loading a Python or Anaconda modulefile), you can view a list of the Python packages installed by typing the following commands.

If you have loaded a Python modulefile:

.. code-block::

   pip list

If you have loaded an Anaconda modulefile:

.. code-block::

   conda list

Using R on Nightingale
-----------------------

Introduction
~~~~~~~~~~~~~~

`R <https://en.wikipedia.org/wiki/R_(programming_language)>`_ is a programming language and software environment for statistical computing and graphics. R and its libraries implement a wide variety of statistical and graphical techniques, such as linear and non-linear modeling, classical statistical tests, time-series analysis, classification, and clustering.

R is easily extensible through functions and extensions. The R community is noted for its active contributions to developing R packages. R packages contain code, data, and documentation in a standardized collection format that R users can install. R and R packages are available via the `Comprehensive R Archive Network (CRAN) <https://cran.r-project.org>`_, a collection of sites that carry the R distribution(s), the contributed extensions, documentation for R, and binaries.

Versions
~~~~~~~~~

See :ref:`installed` for the versions of R installed on Nightingale.

Adding R to Your Environment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You can use a modulefile to load a specific R version into your user environment. 

.. code-block::

   module avail R

To load a specific version, you will need to load the corresponding module. See :ref:`modules` for more information about modules.

Load the *latest* version of R available on Nightingale:

.. code-block::

   module load R

Installing Add-on Packages
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Any R add-on packages not available in the system installation can be installed from the CRAN in a user-specified location. 
You must have write access to the location.

Installation Command Syntax
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To install R packages, all that is needed is the package name; you can also specify additional information, such as installation location and the repository.
The install R packages commands is ``install.packages()``. Two example installations specifying **Package Name**, **Location**, and **Repository** are shown below.

Install the package downloaded (**package name**) from the specified repository (**Repository URL**) into the specified location (**/path/to/r_libraries**):

.. code-block::

   install.packages('package_name', '/path/to/r_libraries', 'Repository URL')

Install the local package (**package_name.tar.gz**) into the specified location (**/path/to/r_libraries**), specifying no repository (**repos = NULL**):

.. code-block::

   install.packages('package_name.tar.gz', '/path/to/r_libraries', repos = NULL)

When the installation location and the repository URL are not specified, R packages are installed in a default location, and the R installation process prompts you to choose from a list of repositories. R packages downloaded manually from the CRAN can be installed by specifying the local file name and omitting the repository URL (specifying NULL).

Using Rscript
~~~~~~~~~~~~~~

You can use the ``rscript`` command to run R commands without starting an R session. As a scripting frontend for R, Rscript enables using R via shell scripts and scripting applications.

The example below shows step-by-step the commands you can run on Nightingale. In these steps, **~/Rlibs** is used for the location to install your user-specific add-on packages and the tilde **~** means your home directory (**$HOME**).

.. note::
   This example uses the Bash shell. The command syntax may differ when using a different shell.

#. Set the **HTTPS_PROXY** environment variable (if you have not already done so):

   .. code-block::

      export HTTPS_PROXY=http://ache-proxy.ncsa.illinois.edu:3128

#. Create a directory for your R packages:

   .. code-block::

      mkdir ~/Rlibs

#. Load the R modulefile:

   .. code-block::
 
      module load R/4.2.0

#. Set the R library environment variable (**R_LIBS**) to include your R package directory:

   .. code-block::

      export R_LIBS=~/Rlibs:$R_LIBS

#. Use the ``install.packages()`` command to install your R package:

   .. code-block::

      Rscript -e "install.packages('RCurl', '~/Rlibs', 'https://cran.r-project.org')"

If the environment variable **R_LIBS** is not set and a directory is not specified with the ``install.packages()`` command, then R packages will be installed under **~/R/x86_64-unknown-linux-gnu-library** by default (this R subdirectory structure is created automatically). The **R_LIBS** environment variable will need to be set every time when logging into Nightingale if your R package location is to be visible to an R session. You can add the following code to your **~/.bashrc** file to remove the need to set the **R_LIBS** environment variable with every login session to Nightingale:

.. code-block::

   if [ -n $R_LIBS ]; then
         export R_LIBS=~/Rlibs:$R_LIBS
   else
         export R_LIBS=~/Rlibs
   fi
 
Warnings and Error Messages
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If the name of a package is misspelled or the R package is not available in the current CRAN, an error message similar to the following will be generated:

.. code-block::

   [ng-login01 ~]$ Rscript -e "install.packages('phybase','~/Rlibs', 'http://ftp.ussg.iu.edu/CRAN')"
   Warning message:
   package 'phybase' is not available (for R version 3.2.2)
 
Searching the CRAN site for your desired R package may provide links to archived versions that are not available in the current CRAN. 
In this case, the specific archived R package can be downloaded and installed from the local file using the same command but omitting the repository URL (specifying NULL).

Some R packages have dependencies that are required to be installed first, and will generate an error message similar to:

.. code-block::

   [ng-login01 ~]$ Rscript -e "install.packages('phybase_1.1.tar.gz', '~/Rlibs',  repos = NULL)"
   ERROR: dependency 'ape' is not available for package 'phybase'
   * removing '/home/jdoe/Rlibs/phybase'
   Warning message:
   In install.packages("phybase_1.1.tar.gz", repos = NULL) :
     installation of package 'phybase_1.1.tar.gz' had non-zero exit status
 
Installing the dependency first and then the desired R package resolves this issue.

Viewing Installed R Packages
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You can use the ``library()`` command to view all your user and system-installed R packages (user-installed packages are only visible to R when the **$R_LIBS** environment variable is set):

.. code-block::

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

|

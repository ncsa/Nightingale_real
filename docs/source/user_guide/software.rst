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
You can use :ref:`module commands <modules>` to add this software to your software environment.

==============================================================================   ========================
Software                                                                         Version
==============================================================================   ========================
Anaconda_                                                                        2022.05  (Python 3.9.12)
`awscli <https://aws.amazon.com/cli/>`_                                          2.4.16
`CUDA <https://docs.nvidia.com/cuda/archive/11.4.2/>`_                           11.4.2
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
   - In the module commands below, replace ``modulefile``, ``modulefile2``, ``oldmod``, and ``newmod`` with the names of the modulefile(s) you are running the command on.

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
|                    | #. Type ``module save``.                                                      |
+--------------------+-------------------------------------------------------------------------------+

For more information on module commands, see the `Environment Modules Documentation <https://modules.readthedocs.io/en/stable/index.html>`_.

Using Python on Nightingale
-----------------------------

Introduction
~~~~~~~~~~~~~~~

Anaconda and Miniconda are specilized distributions of the Python and R programing languages for scientific computing. Anaconda and Miniconda include `Conda <https://en.wikipedia.org/wiki/Conda_(package_manager)>`_, a package and environment management system; this allows you to create numerous environmnets to suit your specific needs.

Versions
~~~~~~~~~

See :ref:`installed` for the versions of Anaconda, and Miniconda installed on Nightingale.

Setting an Environment Variable
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To be able to install additional python packages via Conda, you will need to set the ``HTTPS_PROXY`` environment variable. 
**You will need to set the "HTTPS_PROXY" environment variable every time you log in to the cluster using the following command:**

.. code-block:: 

   export HTTPS_PROXY=http://ache-proxy.ncsa.illinois.edu:3128

To verify that this environment variable is set use the ``echo`` command to output the value of the environment variable.

.. code-block:: 

   echo ${HTTPS_PROXY}

Anaconda and Miniconda are installed on Nightingale. 
One of the main differences between Anaconda and Minconda is the number of packages: 
Anaconda by default installs with over 150 data science packages, and Miniconda by default installs a *subset* of the packages installed by default with Anaconda. 

To enable (use) Anaconda or Miniconda on Nightingale, load the appropriate modulefile. Do not load *both* modulefiles, use *either* Anaconda or Miniconda.

.. code-block::

   module load anaconda3/2022.05

or

.. code-block::

   module load miniconda3/2022.05

Viewing Installed Python Packages
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

After enabling Python in your user environment (by loading a Anaconda or Miniconda modulefile), you can view a list of the Python packages installed with the following command:

.. code-block::

   conda list

Creating your Conda Environment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

We recommend you use the locally installed Conda, so that you can install the specific packages that you need. 
You can have multiple environments with different packages for testing purposes.

#. Create your own conda environment called ``my.conda_env`` with the following command:

   .. code-block::

      conda create -n my.conda_env <package_name>
    
   For example, to create a Conda environment that intalls python and all of its dependencies:

   .. code-block::

      conda create -n my.conda_env python
    
#. To start running Python, you need to activate your Conda environment.

   .. code-block::

      source activate my.conda_env

   When your Conda environment is activated, your prompt should start with:

   .. code-block::

       (my.conda_env)\ [username@ng-login01 ~]$
    
#. Use the following command to display all known Conda environments:

   .. code-block::

      conda info -e

   An asterisk (*) will appear on the line of the Conda environment that is currently active.

#. To make sure you have the latest version of Python in your environment, install Python using the ``conda-forge`` channel.

   .. code-block::

      conda install python --channel conda-forge

#. When you're ready, **exit** your conda environment with the following command:

   .. code-block::

      conda deactivate

   You should now see your default prompt, which indicates that your conda environment has been deactivated.

Complete Example of Creating a Conda Environment  
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The following list of commands will create a conda environment, built around the package `PyTorch <https://pytorch.org/docs/stable/index.html>`_, in your home directory.

.. code-block::

   export HTTPS_PROXY=http://ache-proxy.ncsa.illinois.edu:3128
   cd ${HOME}
   module load anaconda3/2022.05
   export CONDA_PKGS_DIRS="${HOME}/.conda/pkgs"
   conda create -n my.pytorch pytorch
   conda info -e
   source activate my.pytorch
   conda info -e
   conda list
 
Running the command ``conda deactivate``, will deactivate the conda environment created by the above example. 

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

Load the *latest* version of R available on Nightingale with the following command:

.. code-block::

   module load R

Installing Add-on Packages
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Any R add-on packages not available in the system installation can be installed from the CRAN in a user-specified location. 
You must have write access to the location.

Installation Command Syntax
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To install R packages, you only need the package name; you can also specify additional information, such as installation location and the repository.
The install R packages commands is ``install.packages()``. Two example installations specifying **Package Name**, **Location**, and **Repository** are shown below.

- Install the package downloaded (``package name``) from the specified repository (``Repository URL``) into the specified location (``/path/to/r_libraries``):

  .. code-block::

     install.packages('package_name', '/path/to/r_libraries', 'Repository URL')

- Install the local package (``package_name.tar.gz``) into the specified location (``/path/to/r_libraries``), specifying no repository (``repos = NULL``):

  .. code-block::

     install.packages('package_name.tar.gz', '/path/to/r_libraries', repos = NULL)

When the installation location and repository URL are not specified, R packages are installed in a default location, and the installation process prompts you to choose from a list of repositories. R packages downloaded manually from the CRAN can be installed by specifying the local file name and omitting the repository URL (specifying ``NULL``).

Using Rscript
~~~~~~~~~~~~~~

You can use the ``rscript`` command to run R commands without starting an R session. As a scripting frontend for R, Rscript enables using R via shell scripts and scripting applications.

The example below shows step-by-step the commands you can run on Nightingale. In these steps, ``~/Rlibs`` is used for the location to install your user-specific add-on packages and the tilde ``~`` means your home directory (``$HOME``).

.. note::
   This example uses the Bash shell. The command syntax may differ when using a different shell.

#. Set the ``HTTPS_PROXY`` environment variable (if you have not already done so):

   .. code-block::

      export HTTPS_PROXY=http://ache-proxy.ncsa.illinois.edu:3128

#. Create a directory for your R packages:

   .. code-block::

      mkdir ~/Rlibs

#. Load the R modulefile:

   .. code-block::
 
      module load R/4.2.0

#. Set the R library environment variable (``R_LIBS``) to include your R package directory:

   .. code-block::

      export R_LIBS=~/Rlibs:$R_LIBS

#. Use the ``install.packages()`` command to install your R package:

   .. code-block::

      Rscript -e "install.packages('RCurl', '~/Rlibs', 'https://cran.r-project.org')"

If the environment variable ``R_LIBS`` is not set and a directory is not specified with the ``install.packages()`` command, then R packages will be installed under ``~/R/x86_64-unknown-linux-gnu-library`` by default (this R subdirectory structure is created automatically). The ``R_LIBS`` environment variable will need to be set every time when logging into Nightingale if your R package location is to be visible to an R session. You can add the following code to your ``~/.bashrc`` file to remove the need to set the ``R_LIBS`` environment variable with every login session to Nightingale:

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
In this case, the specific archived R package can be downloaded and installed from the local file using the same command but omitting the repository URL (specifying ``NULL``).

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

You can use the ``library()`` command to view all your user and system-installed R packages (user-installed packages are only visible to R when the ``$R_LIBS`` environment variable is set):

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

.. _jupyterlab:

Launching a JupyterLab Session
--------------------------------

Launch a JupyterLab session in a web browser with the following steps.

#. Log in to ``ng-login01``. (Replace ``username`` with your Nightingale username.)

   .. code-block:: terminal

      ssh username@ng-login01.ngale.internal.ncsa.edu

#. On the login node, run the following commands:

   .. code-block:: terminal

      module load anaconda3/2024.02 ng_scripts/0.4

   .. code-block:: terminal

      ng_jupyter_lab_tunnel.bash 

#. Leave your first terminal open, and open a **second terminal** on your local machine. 

#. In the second terminal, run the following command and complete the login prompts. (Replace ``username`` with your Nightingale username in **both** places.)

   .. code-block:: terminal

      ssh -J username@ngale-bastion-1.ncsa.illinois.edu -L 13000:localhost:13000 username@ng-login01.ngale.internal.ncsa.edu

#. Open a web browser on your local machine and paste the URL at the end of the output of ``ng_jupyter_lab_tunnel.bash`` in the **first terminal** and into the web browser.

   A JupyterLab session will launch in the web browser.

   .. figure:: images/software/jupyterlab-url-terminal.jpg
      :alt: Example terminal windows logged into Nightingale with the output URL highlighted.
      :width: 1000

   .. figure:: images/software/jupyterlab-url-browser.jpg
      :alt: Web browser showing example output URL.
      :width: 1000

   .. figure:: images/software/jupyterlab.png
      :alt: JupyterLab session opened in a web browser.
      :width: 1000

|

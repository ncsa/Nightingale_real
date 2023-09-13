
Adding Software
===============================

Software Already Installed
-----------------------------

Before attempting to install a software package (or requesting that it
be installed for you) you should make sure that it isn’t already
available on the system using the “module avail” command. You can use
the module command suite to configure your individual login session with
software that's available on the system but not immediately available
(loaded). See the page for details.

Where To Install Software
--------------------------

| For software that's not installed on the system already, users of the
  Nightingale system can only install software into user space which are
  the directories that they have write access to such as their home
  directory, scratch space, and project spaces that they have been given
  access to.
| Only the system administrators can install software in system spaces
  which require root access to change. Users may have been able to use
  “privileged” tools such as sudo, yum, and apt-get previously on other
  systems, but they are not available to users on Nightingale for
  security reasons.

We recommend that users install software packages and libraries into the
project spaces that they have access to. The software will then be
available to the rest of their team. They can request access to these
spaces from the project’s owners. Home directories have limited disk
quotas so we don’t recommend using that space for software installation.

Scratch space can be useful for trying out an installation but it not a
good long term solution since it is volatile storage and can be deleted
at any time. [scratch purge policy]

Network Access
-----------------

Nightingale nodes don't have access to the outside internet, which the
above auto-install tools require to work. To run those, you'll generally
need to run this command on your command line before running any of
these tools:

::

    export HTTPS_PROXY=http://ache-proxy.ncsa.illinois.edu:3128

This sets the auto-install tool to access the outside internet through a
network proxy, which allows connections to limited outside network
addresses.

Quotas
--------

There currently is no user command that will list your quotas or what
your storage situation is. We will update this page when those commands
are implemented.

Auto-installing Tools
------------------------

The "Conda" software install tool is available to users on Nightingale.
You must first load the "anaconda" module. However, due to network
security restrictions on Nightingale, only some Conda "channels" are
available for installation. If you think you need something in a Conda
channel that doesn't seem to work, send us a ticket. It may be possible
to enable new Conda channels, but all such requests will be made on a
case-by-case basis.

We are working on getting a spack-based software installation on
Nightingale. However, we don't have that ready because of the network
restrictions in place on Nightingale. We will change the documentation
on this page once we have a working version of spack on Nightingale.

Conda
------

Conda is an open-source, cross-platform, language-agnostic package
manager and environment management system. It is a popular package
manager for Python and R. Here is how you can start using Conda on
Nightingale.

Setting an environment variable
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To be able to install additional python packages via Conda, you will
need to set the HTTPS_PROXY environment variable. **You will need to set
the "HTTPS_PROXY" environment variable every time you log in to the
cluster using the following command:**

:: 

    export HTTPS_PROXY=http://ache-proxy.ncsa.illinois.edu:3128



To verify that this environment variable is set use the "echo" command
to output the value of the environment variable.

:: 

    echo ${HTTPS_PROXY}

As long as the variable has a value it will be echoed out. If no value
is set, then an empty line will be displayed instead.

Anaconda (ver 2022.05) and Miniconda (ver 2022.05) are installed on
Nightingale. Essentially one of the main differences between Anaconda
and Minconda is the number of packages: Anaconda by default installs
with over 150 data science packages, whereas Miniconda by default
installs a subset of the packages installed by default with Anaconda. To
enable (make use of) Anaconda or Miniconda on Nightingale, just load the
appropriate modulefile.

::

    module load anaconda3/2022.05

or

::

    module load miniconda3/2022.05

**Note:** Do not load both modulefiles. Use either Anaconda or
Miniconda.

List the python packages that are already available on the cluster.

::

    conda list

Creating your Conda environment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

We recommend you use the locally installed Conda, so that you can
install the specific packages that you need. You can have multiple
environments with different packages for testing purposes.

Users can use the following command to create their ownconda environment
called 'my.conda_env'. If you wish, you can set a different name.

::

    conda create -n my.conda_env <package_name>
    
For example, to create a Conda environment (that intalls python and all
of its dependencies):

::

    conda create -n my.conda_env python
    

To start running Python, you need to activate your Conda environment.

::

    source activate my.conda_env

Now, you should be in your Conda environment, and your prompt should
start with:

::

    **(my.conda_env)**\ [username@ng-login01 ~]$
    

Use the following command to display all known Conda environments:

::

    conda info -e

An asterisk (*) will appear on the line of the Conda environment
that is currently active.

To make sure you have the latest version of Python in your environment,
install Python using the conda-forge channel.

::

    conda install] python --channel conda-forge

To exit you conda environment type the following command:

::

    conda deactivate

You should now see your default prompt, which indicates that your conda
environment has been deactivated.

| 

Installing other packages
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Activate your Conda environment:

::

    source activate my.conda_env

Search for the python package of interest and display associated
information.

::

    conda search 

Install a selected python package:

::

    conda install <package_name>

or

::

    conda install <pacakge_name> --channel <channel_name>
    

View what python packages are installed:

::

    conda list

R
---

`R is a programming language for statistical computing <https://www.r-project.org/>`_ 
and graphics supported by the R Core Team and the R Foundation for
Statistical Computing.  R version 4.2.0 is currently installed on
Nightingale.

To enable (make use of) R on Nightingale, just load the modulefile.

::

    module load R/4.2.0`

To start R, simply type R in the terminal.

::

    R

The program will open *within* the terminal window. Type 'demo()' for
some demos, 'help()' for on-line help, 'q()' to quit R. If you use
functions like'plot()' in R, your graph will open in a separate window.
This is assuming you use MobaXterm or another X server.

You can also run your R scripts in the background by using the Rscript
command.

::

    Rscript my_script.R

You can use a text editor (Ex. nano, vi, etc ...) to create the script
files on the cluster or you can use R Studio on your PC/Mac to create
the script and then upload the file to the cluster.

| 

Viewing Installed R Packages
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The library() command can be used to view all user and system installed R
packages (user installed packages are only visible to R when
the${R_LIBS}environment variable is set).

::

    Rscript -e "library()"`

Installing Additional R Packages
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Additional user specific R packages not listed in Nightingale's system
installation of R can be installed by any Nightingale
user from the “Comprehensive R Archive Network” (CRAN). User
  Installation Steps for R packages below:

Set the HTTPS_PROXY environment variable (if you have not already done
so).

::

    export HTTPS_PROXY=http://ache-proxy.ncsa.illinois.edu:3128

Create a directory 'my.Rlibs' for your R packages. If you wish, you can
use a different name.

::

    mkdir ${HOME}/my.Rlibs

Load the R modulefile (if you have not already done so).

::

    module load R/4`.2.0`` 

Set the R library environment variable (R_LIBS) to include your R
package directory

::

    export R_LIBS=${HOME}/my.Rlibs

Use the "install.packages" function to install your R package.

::

    Rscript -e "install.packages('RCurl', '${HOME}/my.Rlibs', 'https://cran.r-project.org')"

**Note:**\ "RCurl" is just the name of the R package used for the
example above. Users, should use the specific R package
(https://cran.r-project.org/web/packages/available_packages_by_name.html)
that they are interested in.

(If the environment variable **R_LIBS** is not set and a directory is
not specified with the "install.packages" function, then R packages
will be installed under "${HOME}/R/x86_64-unknown-linux-gnu-library"
by default.  This R subdirectory structure is created automatically.)

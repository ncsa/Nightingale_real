######
Conda
######

Conda is an open-source, cross-platform, language-agnostic package
manager and environment management system. It is a popular package
manager for Python and R. Here is how you can start using Conda on
Nightingale.

Setting an environment variable
===============================

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
===============================

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

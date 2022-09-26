###########################
Using Python on Nightingale
###########################

Introduction
============
Python is an interpreted, high-level, general-purpose programming language. Python and Python packages are available via the the `Python Package Index (PyPI) <https://pypi.org/>`_ , which hosts thousands of third-party modules for Python. Both Python’s standard library and the community-contributed modules allow for endless possibilities. Anaconda also provides a Python environment with python packages.

Versions
========
The table below lists the versions of Python installed on the Nightingale.
     
.. list-table:: 

   * - Anaconda 2022.05
   * - Miniconda 2022.05
   * - Python 3.9.5
   * - Python 3.9.12

Adding Python To Your Environment
=================================

Each Python installation on Nightingale has a corresponding modulefile for loading a specific version of 
Python into your software environment. To see the available Python versions type the following on the command line::

   module avail anaconda3

and/or::

   module avail miniconda3

See `Using Modules <modules>`_ for more information about modules.

Installing Python Packages (in user specified locations)
========================================================
 
You must install software/libraries into user write-able locations like your home directory, your group’s project space, or your scratch space. Software installed in scratch space is not permanent and may be removed at any time. We recommend that you install it in your group’s project space instead.

Generally, any Python package not available in the system installation can be 
installed from the `Python Package Index <https://pypi.org/>`_ (PyPI) in a location you specify. 

The following commands will create a minimal clone anaconda environment in your scratch directory, install pytorch, and list the Python packages 
installed (including your own installed packages) in your environment::

  cd ${HOME}
  module load anaconda/2022-May/3
  export ${HOME}/.conda/pkgs
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
=================================

After enabling Python in your user environmnet by loading a Python or Anaconda modulefile, you can view a list of the Python packages 
installed (including your own installed packages) by typing the following commands.

If you have loaded a Python modulfile, type::

   pip list

if you have loaded an Anaconda modulefile, type::

   conda list



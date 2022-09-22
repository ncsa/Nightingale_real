###########################
Using Python on Nightingale
###########################

Introduction
============
Python is an interpreted, high-level, general-purpose programming language..
Python and Python packages are available via the “The Python Package Index” (PyPI), which hosts thousands of third-party modules for Python. Both Python’s standard library and the community-contributed modules allow for endless possibilities.
Anaconda also provides a Python environment with python packages

Versions
========
The table below list the versions of Python installed on the Nightingale.

.. list-table:: **Python Versions**
   :widths: 25 25 

   * - Anaconda 2022.05
     - Python 3.9.12
   * - Miniconda 2022.05
     - Python 3.9.5

Adding Python To Your Environment
=================================

Each Python installation on the Nightingale has a corresponding modulefile that can be used to load a specific version of 
Python into your user environment. You can see the available versions of Python by typing the following on the command line::

   module avail anaconda3

and/or::

   module avail miniconda3

See the section Managing Your Environment in the User Guide for more information about modules.

Installing Python Packages (in user specified locations)
========================================================

Generally, any Python package not available in the system installation can be 
installed from the `Python Package Index <https://pypi.org/>`_ (PyPI) in a location you specify. You must have write access to the location. 

When installing any software there are a few things to consider:

 - Home directory disk usage quotas.
 - Will the software be used by multiple users in my group? 
   (If so, project space is the **recommended** location to install software.)
 - Does the desired software have dependencies/requirements?
 - Is the prerequisite software already installed?
 
You must install software/libraries into user write-able locations like your home directory, your group’s project space or your scratch space.

Installation Command Syntax
---------------------------

Under Anaconda:

The following commands will create an anaconda environment in your scratch directory.
Please note that software installed in scratch space is not permanent and may be removed at any time. 
We recommend that you install it in your group’s project space instead.

To create a minimal clone anaconda environment type the following::

  cd ${HOME}
  module load anaconda/2022-May/3
  export ${HOME}/.conda/pkgs
  conda create -n my.anaconda python
  conda info -e
  source activate my.anaconda
  conda info -e
  conda install pytorch
  conda list
 
To deactivate the anaconda environment just type::

 conda deactivate

To create a complete clone anaconda environment replace::

 conda create -n my.anaconda python
 
with::

 conda create -n my.anaconda anaconda


Viewing Installed Python Packages
=================================

After enabling Python in your user environmnet by loading a Python or Anaconda modulefile, you can view a list of the Python packages 
installed (including your own installed packages) by typing::

   pip list

if you have loaded a Python modulfile or by typing::

   conda list

if you have loaded an Anaconda modulefile.

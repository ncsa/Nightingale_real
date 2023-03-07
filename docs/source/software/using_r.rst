######################
Using R on Nightingale
######################

Introduction
============

R is a programming language and software environment for statistical computing and graphics. It is an interpreted language typically accessed through a command-line interpreter. R and its libraries implement a wide variety of statistical and graphical techniques, such as linear and non-linear modeling, classical statistical tests, time-series analysis, classification, and clustering.

R is easily extensible through functions and extensions. The R community is noted for its active contributions to developing R packages. R packages contain code, data, and documentation in a standardized collection format that R users can install. R and R packages are available via the `Comprehensive R Archive Network (CRAN) <https://cran.r-project.org>`_, a collection of sites that carry identical material, consisting of the R distribution(s), the contributed extensions, documentation for R, and binaries.

Versions
========

The table below lists the versions of R currently installed on Nightingale.

+---------+
| Version |
+---------+
| R 4.2.0 |
+---------+

Adding R to Your Environment
============================

You can use a module file to load a specific R version into your user environment.::

   module avail R

The latest version of R available on the Nightingale can be loaded into your environment by typing::

   module load R

To load a specific version, you will need to load the corresponding module. (See `Using Modules <modules>`_ for more information about modules.)

Installing Add-on Packages
==========================

Any R add-on package not available in the system installation can be installed from the CRAN in a user-specified location. 
You must have write access to the location.

Installation Command Syntax
===========================

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
=============

You can use the rscript command to run R commands without starting an R session. As a scripting front end for R, Rscript enables using R via shell scripts and scripting applications.

The examples below show step-by-step the commands you can run on Nightingale. In these steps, ~/Rlibs is used for the location to install user-specific add-on packages (The tilde "~" means the users' home directory—i.e. $HOME).

**Note:** These examples use the BASH shell. The command syntax may differ when using a different shell.

**Step 1:** Set the HTTPS_PROXY environment variable (if you have not already done so).

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
===========================

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
============================

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

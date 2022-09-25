##################################
Managing Your Environment
##################################

Using Modules
=============

Nightingale uses a set of module commands that enable users to configure
their software environment. Essentially, you can turn access to certain 
software on or off by "loading" or "unloading" a modulefile that adds
or removes the software's configuration in your user environment). The 
table below shows the most common module commands you will need on 
Nightingale.

+--------------------+-------------------------------------------------+
| Command            | Description                                     |
+--------------------+-------------------------------------------------+
| module avail       | Lists the modules that are available. If you    |
|                    | are looking for a piece of software but typing  |
|                    | the command to run it gets you a "command not   |
|                    | found" error, then loading the modulefile for   |
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
| module display     | |                                               |
| *modulefile*       |                                                 |
|                    | Display (or show) the changes that loading the  |
| or                 | modulefile will make to the user environment.   |
|                    |                                                 |
| module show        |                                                 |
| *modulefile*       |                                                 |
+--------------------+-------------------------------------------------+
| module load        | Loads a modulefile [or modulefiles] into your   |
| *modulefile (      | current shell environment (see "module avail"   |
| modulefile2        | above to get a list)                            |
| modulefile3 ...)*  |                                                 |
+--------------------+-------------------------------------------------+
| module unload      | Unloads a modulefile; if you unload a           |
| *modulefile*       | modulefile you had previously loaded, then the  |
|                    | software is no longer available to you (in your |
|                    | current shell environment).                     |
+--------------------+-------------------------------------------------+
| module swap        | Unloads one *modulefile1* and loads another     |
| *modulefile1       | *modulefile2*. This is typically used to change |
| modulefile2*       | the version of a modulefile that you have       |
|                    | loaded.                                         |
+--------------------+-------------------------------------------------+
| module save        | If you have modulefiles that you want to load   |
|                    | every time you log in, then you can set up your |
|                    | account so that they are loaded every time you  |
|                    | log in without you having to type the "module   |
|                    | load" every time. Do this by first loading the  |
|                    | modulefiles you always want to have loaded.     |
|                    | Then type "module save". The system will save   |
|                    | your current module list as your default. When  |
|                    | you log in the next time, these modulesfiles    |
|                    | will already be loaded.                         |
+--------------------+-------------------------------------------------+

| 

**Notes:** 

 - Modules are independent of the user’s shell, so any shell (bash,
   tcsh, ksh, etc ...) can use the same commands to modify their current
   user environment.
 - Order is important. With each module load, the changes are
   prepended to your current user environment paths.

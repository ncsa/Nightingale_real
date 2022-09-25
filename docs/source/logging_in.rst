########################
Logging Onto Nightingale
########################

Once you have obtained an account on Nightingale, you can log on using an SSH (Secure Shell) client on your local desktop or laptop. 
Because of the added security for Nightingale, you will first log onto Nightingale's secure node and then log onto a general access login node 
or, for groups that have them, a specialized interactive node. The hostnames for these login nodes are listed below.

**Secure Node Hostname**::

   ngale-bastion-1.ncsa.illinois.edu 

**General Access Login Nodes Hostnames**::

   ng-login01.ngale.internal.ncsa.edu
   ng-login02.ngale.internal.ncsa.edu

**Specialized Interactive Node Hostname**::

   <ng-yourgroup01>.ngale.internal.ncsa.edu

where <ng-yourgroup01> is the name of your allocation group. 

**Note:** You will be informed if your allocation has a Specialized Interactive node.
All Nightingale users have access to the general access login
nodes. Please be aware that the general access head nodes are a shared resource for all 
system users, and their use should be limited to editing, compiling, and building your programs.

**General Log in Process**

You can log onto Nightingale by following these steps:

1. If not on campus, connect to the campus VPN. (`Instructions for installing the campus VPN <https://answers.uillinois.edu/illinois/98773>`_)
2. SSH to the secure node ngale-bastion-1.ncsa.illinois.edu.
3. Enter your NCSA username and password.
4. Enter '1' to send a push to the Duo app on your smartphone.
5. Approve the request on your phone.
6. SSH to your login node using the appropriate hostname (see above).

Below is a sample SSH command line to log into Nightingale's secure node::

   ssh <username>@ngale-bastion-1.ncsa.illinois.edu

where <username> is the username you created for your NCSA identity. After entering the ssh command, you will be prompted to enter your password, followed by a prompt to send a push to the Duo app. After you have approved the push, you may enter the SSH command using the hostname of your login node.

SSH Clients
===========

A variety of SSH-based clients are available for accessing Nightingale from your local system. Which one you use depends on your workstation's operating system. These are described in the sections below.

**Microsoft Windows**

When using the Microsoft Windows operating system, you can use the built-in SSH Client in Windows (version 10 and above) or select from several freely available third-party SSH clients. These typically provide a Graphical User Interface rather than a command-line interface. `PuTTY <http://www.chiark.greenend.org.uk/~sgtatham/putty/>`_ is a popular choice, and `MobaXterm <http://mobaxterm.mobatek.net/>`_ is another one.

**Mac OS X**

Mac OS X comes with a built-in open-source version of SSH called OpenSSH. You can access it via the Terminal application.  `PuTTY <http://www.chiark.greenend.org.uk/~sgtatham/putty/>`_ is also available for Mac OS X.

**Linux**

The Linux operating system has SSH built-into it. You use the Linux terminal application to connect via SSH.  `PuTTY <http://www.chiark.greenend.org.uk/~sgtatham/putty/>`_ is also available for Linux.

Account Administration
======================

Account and project administration, such as resetting your password or adding someone to a project, is 
managed by the NCSA Identity and Group Management tools. Please see the 
`NCSA Allocation and Account Management documentation page <https://wiki.ncsa.illinois.edu/display/USSPPRT/NCSA+Allocation+and+Account+Management>`_ for more information.

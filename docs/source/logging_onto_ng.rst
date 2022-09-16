========================
Logging Onto Nightingale
========================

Once you have completed the steps described in Getting Access to Nightingale, you can log on using an SSH (Secure Shell) client on your local desktop or laptop. You will log onto Nightingale's secure node first and then log onto a general access login node or, for groups that have them, a specialized interactive node. The hostnames for these login nodes are listed below.

Hostnames
~~~~~~~~~~~~~~~~~~~~

**Secure Node**

- ngale-bastion-1.ncsa.illinois.edu 

**General Access Login Nodes**

-  ng-login01.ngale.internal.ncsa.edu
-  ng-login02.ngale.internal.ncsa.edu

**Specialized Interactive Nodes**

- <ng-yourgroup01>.ngale.internal.ncsa.edu

where <ng-yourgroup01> is the name of your allocation group. 

**Note:** You will be informed if your allocation has a Specialized Interactive node.
All Nightingale users have access to the general access login
nodes. Please be aware that the general access head nodes are a shared resource for all 
system users, and their use should be limited to editing, compiling, and building your programs.

General Instructions 
~~~~~~~~~~~~~~~~~~~~~
You can log onto Nightingale by following these steps:

1. If not on campus, connect to the campus VPN
2. SSH to the secure node ngale-bastion-1.ncsa.illinois.edu 
3. Enter your NCSA username and password
4. Enter '1' to send a push to the Duo app on your smartphone
5. Approve the request on your phone
6. SSH to your login node using the appropriate hostname (see above)

**NOW POINT TO PAGES GIVING MORE DETAIL FOR USERS WHO DO NOT KNOW HOW TO SSH, ETC**

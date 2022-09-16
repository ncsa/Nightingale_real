=====================
Accessing the System
=====================

Getting an Account
~~~~~~~~~~~~~~~~~~
To access Nightingale you must first get an NCSA Identity (username and password) and request access from Nightingale 
administrators. Once approved, you will be given instructions on how to be added to NCSA's HIPPA-Covered Entity. The three 
steps below explain this process.

**1. Create an NCSA Identity**

Before requesting Nightingale access, you need an NCSA identity. You can skip this step if you already have an NCSA identity. 
If you don’t remember your password, you can reset it using this link: https://identity.ncsa.illinois.edu/.

- **To create an NCSA identity**, go to this invite link: https://go.ncsa.illinois.edu/ngale_identity.

**Note:** In addition to creating a new account, this process will automatically enroll you into NCSA's Duo multi-factor 
authentication (https://go.ncsa.illinois.edu/2fa), which is required to log into Nightingale.

**2. Request Nightingale Access**

- **To request Nightingale access**, send an email to  `help+hipaa@ncsa.illinois.edu <mailto:help+hipaa@ncsa.illinois.edu>`_ that 
includes your NCSA identity, your University UIN, and a brief description of why you want the access. Please attach your training certificate if you completed Regulated Sensitive Data training less than a year ago (HIPPA or otherwise).

**3. Get Added to NCSA's HIPPA-Covered Entity**

The University of Illinois’ HIPAA Privacy and Security Directive requires that all members of a covered entity complete HIPAA training on an annual basis and perform endpoint disk encryption of portable devices (like laptops) used to access, process, or store HIPAA-regulated sensitive data. Your email request in Step 2 starts the process of getting added to NCSA's HIPAA Covered Entity required to access Nightingale.

- **To get added to NCSA's HIPPA-Covered Entity**, follow the instructions in the response to the email you sent in Step 2. These instructions will include information on how to access the HIPAA training and submit your completion certificate and perform the disk encryption. (The instructions will connect you with NCSA personnel who will guide you through the encryption process.)

**Note:** You may request an exemption from the encryption requirement in cases such as if you plan to use an on-site work desktop.


Logging Onto Nightingale
~~~~~~~~~~~~~~~~~~~~

Once you have obtained an account on Nightingale, you can log on using an SSH (Secure Shell) client on your local desktop or laptop. 
Because of the added security for Nightingale, you will first log onto Nightingale's secure node and then log onto a general access login node 
or, for groups that have them, a specialized interactive node. The hostnames for these login nodes are listed below.

**Secure Node Hostname**

- ngale-bastion-1.ncsa.illinois.edu 

**General Access Login Nodes Hostnames**

-  ng-login01.ngale.internal.ncsa.edu
-  ng-login02.ngale.internal.ncsa.edu

**Specialized Interactive Node Hostname**

- <ng-yourgroup01>.ngale.internal.ncsa.edu

where <ng-yourgroup01> is the name of your allocation group. 

**Note:** You will be informed if your allocation has a Specialized Interactive node.
All Nightingale users have access to the general access login
nodes. Please be aware that the general access head nodes are a shared resource for all 
system users, and their use should be limited to editing, compiling, and building your programs.

**General Log in Instructions**

You can log onto Nightingale by following these steps:

1. If not on campus, connect to the campus VPN. (`Instructions for installing the campus VPN <https://answers.uillinois.edu/illinois/98773>`_)
2. SSH to the secure node ngale-bastion-1.ncsa.illinois.edu.
3. Enter your NCSA username and password.
4. Enter '1' to send a push to the Duo app on your smartphone.
5. Approve the request on your phone.
6. SSH to your login node using the appropriate hostname (see above).

**Link to SSH tools**

Account Administration
~~~~~~~~~~~~~~~~~~~~~~

Account and project administration, such as resetting your password or adding someone to a project, is 
managed by the NCSA Identity and Group Management tools. For more information, please see the 
`NCSA Allocation and Account Management documentation page <https://wiki.ncsa.illinois.edu/display/USSPPRT/NCSA+Allocation+and+Account+Management>`_.

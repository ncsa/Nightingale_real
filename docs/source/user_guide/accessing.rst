.. _access:

Accessing the System
=========================

Getting an Account
-------------------

To access Nightingale, your project needs to have a *project group* set up with access to Nightingale, and associated with the various resources that you need to use. The project's Principal Investigator (PI) sets up the project group, and the PI's user login account will be the first login account attached to the project group. The PI must have an NCSA Identity (username and password) or get one, and request access from Nightingale administrators. This page covers that process.  

The project PI will need to follow the process of creating the project group, and themselves go through the training process and be added to the HIPAA Covered Entity. Other users on the project will just need to follow the training and Covered Entity process. This page covers both processes.  

Create an NCSA Identity
~~~~~~~~~~~~~~~~~~~~~~~~~~

Before requesting Nightingale access, both PIs and individual users need an NCSA identity. **Skip this step if you already have an NCSA identity**; if you don't remember your password, you can reset it on the `NCSA Identity and Access Management webpage <https://identity.ncsa.illinois.edu/>`_.

To create an NCSA identity, go to this `invite link <https://go.ncsa.illinois.edu/ngale_identity>`_ and click the "Register New User and Join" button.

In addition to creating a new account, this process will automatically enroll you into NCSA's Duo multi-factor authentication (https://go.ncsa.illinois.edu/2fa), which is required to log into Nightingale. **This is not the same as the University of Illinois' Duo**. 

.. note::
   
   When you enroll in NCSA Duo, it is very important to create and save two backup codes to use in case you lose your Duo device.  

Discuss Your Project with Nightingale Management
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Individual users don't need to follow this step.**  Before getting your project added to the Nightingale system, a PI will need to discuss your project, its needs, your expectations, and what Nightingale access can get you. To begin that conversation, please fill out the `NCSA XRAS <https://xras-submit.ncsa.illinois.edu/opportunities/531957/requests/new>`_. Someone from the Nightingale project will contact you via email within a few days of filling out this form. That person will begin the process of creating your project group.  

After your project group is created, Nightingale administrators will create your data storage directories and project group name. The PI will find out about these steps via email. Your group will be assigned an interactive node (shared or exclusive) to log into, and/or if you have batch system access, you'll be assigned a *charge account* to assign your jobs to.  

Being Added to Nightingale Access
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Both PIs creating a new project and individual users joining a project will need to follow these steps to get their user login accounts access to the Nightingale system.  

During this process, *you* are responsible for:

* Becoming part of the NCSA HIPAA Covered Entity

  * This will involve taking training specific to the type of data that you'll be handling on Nightingale
  
  * You may need to submit your training certificate to a web form to become part of the covered entity

* Making sure all devices that you'll log into Nightingale from have an encrypted hard drive

Logging Onto Nightingale
--------------------------

Once you have obtained an account on Nightingale, you can log on using an SSH (Secure Shell) client on your local desktop or laptop. 
Because of the added security for Nightingale, you'll first log onto Nightingale's secure node and then log onto a general access login node or, for groups that have them, a specialized interactive node. The hostnames for these login nodes are listed below.

Node Hostnames
~~~~~~~~~~~~~~~

Secure Node Hostname
$$$$$$$$$$$$$$$$$$$$$$

.. code-block::

   ngale-bastion-1.ncsa.illinois.edu 

General Access Login Nodes Hostnames
$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$

.. code-block::

   ng-login01.ngale.internal.ncsa.edu
   ng-login02.ngale.internal.ncsa.edu

Specialized Interactive Node Hostname
$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$

.. code-block::

   ng-<yourgroup>01.ngale.internal.ncsa.edu

where ng-<yourgroup>01 is the name of your allocation group. 

.. note::

   - Your principal investigator can inform you if your allocation has a specialized interactive node and its hostname.
   - All Nightingale users have access to the general access login nodes. Please be aware that these nodes are a shared resource for all system users, and you should limit your use of them to editing, compiling, and building your programs.

General Log in Process
~~~~~~~~~~~~~~~~~~~~~~~

You can log onto Nightingale by following these steps:

#. If not on campus, connect to the campus VPN. `Instructions for installing the campus VPN <https://answers.uillinois.edu/illinois/98773>`_.
#. SSH to the secure node ngale-bastion-1.ncsa.illinois.edu.
   
   Sample SSH command line to log into the secure node where <username> is the username for your NCSA identity:
   
   .. code-block::

      ssh <username>@ngale-bastion-1.ncsa.illinois.edu

#. Enter your NCSA username and password (you won't see the characters you type for your password).
#. Type ``1`` to send a push to the NCSA Duo app on your smartphone.
#. Approve the push request on your phone.

   After you've approved the push, you'll be at a prompt on the ngale-bastion-1 node that will look similar to:
   
   .. code-block::

      [csteffen@ngale-bastion-1 ~]$

#. SSH to your login node using the appropriate hostname (see above) following this syntax:
   
   .. code-block::

      ssh <your_username>@ng-<yourgroup>01

   For example, if your username is "hirop" and your group name is "biology", then your SSH command would be:
   
   .. code-block::

      ssh hirop@ng-biology03
   
   In this case, you would have been specifically told that "ng-biology03" is the node to use for your computations.

   The two commands above can be combined into one by specifying the bastion host as a *jump* host. The jump host is used to connect to your destination node without needing to interact with it. In this example, user "test1" can log into the Nightingale login node "login01" directly without logging into the bastion host first.
   
   .. code-block::

      ssh -J test1@ngale-bastion-1.ncsa.illinois.edu test1@ng-login01

SSH Clients
------------

SSH (Secure Shell) is a client-server architecture that provides a secure channel over an unsecured network. An SSH client is a program for logging securely into and executing commands on a remote machine. SSH encrypts the data sent over an open network, such as the internet, so that it can't be read by others.

Several SSH-based clients are available for accessing Nightingale. The client you use depends on your workstation’s operating system.

Microsoft Windows
~~~~~~~~~~~~~~~~~~~

You can use the built-in SSH Client in Windows (version 10 and above) or select from several freely available third-party SSH clients. 
These typically provide a Graphical User Interface rather than a command-line interface. `PuTTY <http://www.chiark.greenend.org.uk/~sgtatham/putty/>`_ is a popular choice, `MobaXterm <http://mobaxterm.mobatek.net/>`_ is another one.

Mac OS X
~~~~~~~~~

Mac OS X comes with a built-in open-source version of SSH called OpenSSH. You can access it via the Terminal application. 
`PuTTY <http://www.chiark.greenend.org.uk/~sgtatham/putty/>`_ is also available for Mac OS X.

Linux
~~~~~~~

The Linux operating system has SSH built into it. You use the Linux terminal application to connect via SSH. 
`PuTTY <http://www.chiark.greenend.org.uk/~sgtatham/putty/>`_ is also available for Linux.

Accessing Nightingale using a VPN
-----------------------------------

If you log into Nightingale from the University of Illinois campus, you don't need to use a Virtual Private Network (VPN). To access Nightingale from off campus, you'll need to set up and activate a VPN first. A VPN sends your network traffic over an encrypted channel to a server on a different network, making your traffic originate within that other network. In this case, traffic will effectively originate inside of the University of Illinois, which adds an additional level of security and protection for your connection.  

There are two VPN services that will allow you to log into Nightingale from off campus. The first is the University of Illinois VPN, which members of UIUC campus should use by default. The other is the NCSA VPN, which is available for Nightingale users not associated directly with UIUC.  

.. note::

   If your login freezes when you try to log into Nightingale, this may be your problem.  Please try one of these VPN methods.  

University of Illinois VPN
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If you are a member of the University of Illinois, you can use the `University of Illinois VPN service <https://answers.uillinois.edu/illinois/98773>`_.  You'll need to authenticate to the VPN service itself using your University NetID, password, and 2FA.  

NCSA VPN
~~~~~~~~~

If you don't have a University of Illinois NetID, you'll need to use the `NCSA VPN <https://wiki.ncsa.illinois.edu/display/cybersec/Virtual+Private+Network+%28VPN%29+Service>`_.  

If you have trouble setting up or using either of these VPNs, or have questions, submit a ticket (:ref:`help`).  

Connecting with Terminal, SSH, and XQuartz (for users connecting from Mac OS machines)
----------------------------------------------------------------------------------------

One-time X-windows Software Install
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If you want to use an application from Nightingale and have its windows on your own computer, before logging in, install XQuartz on your Mac OS system. You can `download it here <https://www.xquartz.org/>`_. Most users of Nightingale will want to do this.  

One-time SSH Configuration 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Open the "Terminal" application on your Mac. That presents a black window to you that you can type commands into. At the prompt, type ``cd ~/.ssh`` and then hit **return** or **Enter** (in these instructions, **return** and **Enter** are interchangeable).  

Type ``nano config`` and hit **return**. This will bring you into an editor program that looks like this:

.. code-block::  

    UW PICO 5.09                            File: config                               







    ^G Get Help   ^O WriteOut   ^R Read File  ^Y Prev Pg    ^K Cut Text   ^C Cur Pos    
    ^X Exit       ^J Justify    ^W Where is   ^V Next Pg    ^U UnCut Text ^T To Spell   

This allows you to edit a configuration file that sets up connections to the outside world, so you don't have to type as much all the time. You can copy the lines from the below code block, and then modify them in your window per the instructions below the code block. 

.. code-block::

    Host ngb1
      HostName ngale-bastion-1.ncsa.illinois.edu
      ControlMaster auto
      ControlPath /tmp/ssh_mux_%h_%p_%r
      ControlPersist 5h
      User YOUR_USERNAME

    Host ng-login01
      HostName ng-login01.ngale.internal.ncsa.edu
      ProxyJump ngb1
      User YOUR_USERNAME

After pasting the above lines into the file (using the arrow keys to position your cursor), replace "YOUR_USERNAME" with your NCSA identity username. If you have an interactive node assigned to you, you can add another copy of the last stanza of the configuration file, and in that stanza, replace "ng-login01" with the name of *your* login node.  

For example, a user with username "hirop" with the assigned node "ng-gpu-x07" would have the below configuration file.  

.. code-block::

    Host ngb1
      HostName ngale-bastion-1.ncsa.illinois.edu
      ControlMaster auto
      ControlPath /tmp/ssh_mux_%h_%p_%r
      ControlPersist 5h
      User hirop

    Host ng-login01
      HostName ng-login01.ngale.internal.ncsa.edu
      ProxyJump ngb1
      User hirop
      
    Host ng-gpu-x07
      HostName ng-gpu-x07.ngale.internal.ncsa.edu
      ProxyJump ngb1
      User hirop
      
Once you have finished editing the file, hit **control-O** to write the file. Hit **return** to confirm the file name. Then hit **control-X** to exit the editor, and you are back at the prompt.  
      
Logging Into Nightingale
~~~~~~~~~~~~~~~~~~~~~~~~~~
      
Once the above, one-time, steps are complete, follow the below steps each time you want to log into Nightingale to work.

#. Type the following at the prompt (if you are logging into an interactive node, replace "ng-login01" with the name of that active node):

   ``ssh -X ng-login01``

   You may see a message that begins "The authenticity of host...." and ends with "Are you sure you want to continue connecting (yes/no/[fingerprint])?". You may safely type ``yes`` then hit **return**.  

#. You'll be asked for a password. Enter your NCSA (kerberos) password. You **won't see your characters** echoed back to the screen; just type it blindly.  

#. You'll see a Duo prompt asking for a passcode or for "option 1". You may either:

   - Type ``1``, then your phone Duo will ask you for login confirmation. 
   
   Or 

   - Enter a 6-digit password from the **NCSA** entry of your Duo app.  

#. You'll be asked for your password again; that is again your NCSA password. You again won't see it echoed to the screen; just type it blindly.  

#. You should now be at a prompt that reflects that you are on a Nightingale node. You'll know this because the prompt (the bottom line in your terminal or SSH window) will contain the name of the machine you are working on, and that should begin with "ng-" for "NightinGale". It will look something like this: 

   .. code-block::

      [hirop@ng-gpu-m01 ~] $

   You can load modules and run software and access your files from there.  

Connecting with MobaXterm (for users connecting from Windows machines)
------------------------------------------------------------------------

You can install `MobaXterm <https://mobaxterm.mobatek.net/>`_ on your workstation and use it to connect to Nightingale node using SSH. 
MobaXterm enables an SSH connection and provides other useful utilities you can use when communicating with a cluster, such as file transfer and editing.

Follow the steps below to install MobaXterm and connect to Nightingale. Nightingale has extra security to protect the data stored on it, so configuring this connection is slightly more complicated than other HPC clusters. The difference involves adding the SSH connection to the secure bastion node; this is described in Steps 5 and 6.

One-time setup
~~~~~~~~~~~~~~~

This section is the one-time setup on your Windows machine so that it can connect to Nightingale.  

#. `Download MobaXterm <https://mobaxterm.mobatek.net/download-home-edition.html>`_ and install it on your Windows workstation. 

   You can install either the Portable or Installer edition of MobaXterm. You'll need to have admin privileges to install the Installer edition. 
   The Portable edition does not require admin privileges, to use it just extract the downloaded zip file and click **mobaxterm.exe**.

#. Launch the MobaXterm application and click the **Session** button in the upper left of the window to start an SSH session.

   ..  image:: images/accessing/ng_mxt_session_button.gif
       :alt: MobaXterm initial window with Session button circled.

#. Select **SSH** from the session types displayed and click the **OK** button. 

   ..  image:: images/accessing/XC_01_select_ssh.png
       :alt: MobaXterm Session window with SSH button circled.

   You'll now see an area titled 'Basic SSH Settings.' 

   ..  image:: images/accessing/XC_specify_host_username.png
       :alt: MobaXterm Session window with Basic SSH Settings area displayed.

#. In the **Remote host** text box, enter the name of the login node you want to access (either a general access or interactive node). Then check the **Specify username** box and enter your NCSA Identity username as shown in the following example. 

   ..  image:: images/accessing/XC_specify_host_username2.png
       :alt: MobaXterm Session window with Basic SSH Settings filled in.

#. Click the **Network settings** tab and then click the **SSH gateway (jump host)** button.

   ..  image:: images/accessing/XC_network_settings.png
       :alt: MobaXterm Session window with showing Network settings tab clicked and SSH gateway jump host button displayed.

#. In the configuration window displayed, enter ``ngale-bastion-1.ncsa.illinois.edu`` in the **Gateway host** box and your NCSA username in the **Username** box. Then click the **OK** button. 

   You may see a warning message saying that your remote host identification has changed; click the **Yes** button to continue.

   ..  image:: images/accessing/XC_jump_host_filled_in.png
       :alt: MobaXterm Session window with showing values for the SSH gateway jump host filled in.

#. You should now be back in the Session settings window. Click the **OK** button to initiate your SSH connection. A terminal window will be displayed asking for your password; enter your password and hit **Enter**.

Logging Into Nightingale
~~~~~~~~~~~~~~~~~~~~~~~~~~

Once the above, one-time, steps are complete, follow the below steps each time you want to log into Nightingale to work.

#. Open up MobaXterm. In the left bar, there is a list of 'user sessions'.  Each one is a node that you configured above for logging in. Mouse over the Nightingale node you want to log into, right click, and in the resulting menu, select **execute**. 

#. A window will pop up, asking for your password. This is your NCSA password. As you type it, you'll see a row of *************. Hit **Enter** or click **OK**.

#. A second window will pop up asking for your 2FA code. Open your Duo app, click on the "NCSA" entry (not the "University of Illinois" entry) and type the 6-digit code you see into the window.  As with the password above, you'll see it as **********.  

#. The screen will bring up a black window without a prompt. You may need to wait 30 seconds or a minute here. 

   Then it will ask you for your password. You'll type your NCSA password again. You **won't see your characters** echoed back to the screen; just type it blindly.

#. You should have a prompt at the bottom, and a file window on the left showing your directories on Nightingale, and you are ready to work.  

Account Administration
------------------------

On Nightingale there is an approval process for adding users to the system. To start the process, submit a ticket (:ref:`help`).

Other account and project administration tasks, such as resetting your password, are managed by the NCSA Identity and Group Management tools. 
See the `NCSA Allocation and Account Management documentation page <https://wiki.ncsa.illinois.edu/display/USSPPRT/NCSA+Allocation+and+Account+Management>`_ for more information.

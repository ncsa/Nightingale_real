.. _access:

Accessing the System
=========================

Getting an Account
-------------------

To access Nightingale, your project needs to have a *project group* set up with access to Nightingale, and associated with the various resources that you need to use. The project's Principal Investigator (PI) sets up the project group, and the PI's user login account will be the first login account attached to the project group. The PI must have an NCSA Identity (username and password), or get one, and request access from Nightingale administrators. This page covers that process.  

The project PI will need to follow the process of creating the project group, and themselves go through the training process and be added to the HIPAA Covered Entity. Other users on the project will just need to follow the training and Covered Entity process. This page covers both processes.  

Create an NCSA Identity
~~~~~~~~~~~~~~~~~~~~~~~~~~

Before requesting Nightingale access, both PIs and individual users need an NCSA identity. **Skip this step if you already have an NCSA identity**; if you don't remember your password, you can reset it on the `NCSA Identity and Access Management webpage <https://identity.ncsa.illinois.edu/>`_.

To create an NCSA identity, go to this `Nightingale invite link <https://go.ncsa.illinois.edu/ngale_identity>`_ and click **Register New User and Join**.

In addition to creating a new account, this process will automatically enroll you into `NCSA's Duo multi-factor authentication <https://go.ncsa.illinois.edu/2fa>`_, which is required to log in to Nightingale. **This is not the same as the University of Illinois Duo**. 

.. note::
   
   When you enroll in NCSA Duo, it is very important to create and save two backup codes to use in case you lose your Duo device.  

Discuss Your Project with Nightingale Management
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Individual users don't need to follow this step.**  Before getting your project added to the Nightingale system, a PI will need to discuss your project, its needs, your expectations, and what Nightingale access can get you. To begin that conversation, please fill out and the `NCSA XRAS form <https://xras-submit.ncsa.illinois.edu/opportunities/531957/requests/new>`_. Someone from the Nightingale project will contact you via email within a few days of submitting this form and begin the process of creating your project group.  

After your project group is created, Nightingale administrators will create your data storage directories and project group name. The PI will find out about these steps via email. In the informational email to the PI, your group will be assigned an *interactive node* (shared or exclusive) to log in to and/or if you have batch system access, you will be assigned a *charge account* to assign your jobs to.  

Being Added to Nightingale Access
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

PIs creating a new project and individual users joining a project will need to follow these steps to get a user login account to access the Nightingale system.  

During this process, *you* are responsible for:

  - Becoming part of the NCSA HIPAA Covered Entity. This will involve taking training specific to the type of data that you will be handling on Nightingale. You may need to submit your training certificate to a web form to become part of the covered entity.

  \

  - Making sure all devices that you will log in to Nightingale from have an encrypted hard drive.

Logging in to Nightingale
--------------------------

Once you have obtained an account on Nightingale, you can log on using an SSH (Secure Shell) client on your local desktop or laptop. 
Because of the added security for Nightingale, you will first log in to Nightingale's secure node and then log in to a general access login node or, for groups that have them, a specialized interactive node. The following are the hostnames for these login nodes.

.. _node_hostnames:

Node Hostnames
~~~~~~~~~~~~~~~

Secure Node Hostname
$$$$$$$$$$$$$$$$$$$$$$

.. code-block:: terminal

   ngale-bastion-1.ncsa.illinois.edu 

General Access Login Nodes Hostnames
$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$

.. code-block:: terminal

   ng-login01.ngale.internal.ncsa.edu
   ng-login02.ngale.internal.ncsa.edu

Specialized Interactive Node Hostname
$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$

.. code-block:: terminal

   NODENAME.ngale.internal.ncsa.edu

``NODENAME`` will be something of the form ``ng-ai22``, ``ng-gpu-h35``, or ``ng-gpu-m37``. 

.. note::

   - Your PI can inform you if your allocation has a specialized interactive node and if so, its hostname.
   - All Nightingale users have access to the general access login nodes (ng-login01 and ng-login02). Please be aware that these nodes are a shared resource for all system users, and you should limit your use of them to editing, compiling, and building your programs.

General Log in Process
~~~~~~~~~~~~~~~~~~~~~~~

To log in to Nightingale, you first SSH to the secure node and then SSH to your login node. These are the steps:

#. If you are not on campus, connect to the University of Illinois VPN or NCSA VPN (see :ref:`access_vpn`).
#. SSH to the secure node ``ngale-bastion-1.ncsa.illinois.edu``. Replace ``<your_username>`` with your NCSA identity username.
   
   .. code-block:: terminal

      ssh <your_username>@ngale-bastion-1.ncsa.illinois.edu

#. Enter your NCSA username and password. Note, the terminal will not show your password (or placeholder symbols such as asterisks [*]) as you type.
#. Enter ``1`` to send a push to the NCSA Duo app on your smartphone.
#. Approve the push request on your phone.

   After you have approved the push, you will be at a prompt on the ``ngale-bastion-1`` node that will look similar to:
   
   .. code-block:: terminal

      [<your_username>@ngale-bastion-1 ~]$

#. SSH to your login node using the appropriate :ref:`hostname <node_hostnames>`, following this syntax:
   
   .. code-block:: terminal

      ssh <your_username>@ng-<node_type><node_number>

   For example, this is the ``ssh`` command for a user with the username ``hirop`` and the node name ``CPU``:
   
   .. code-block:: terminal

      ssh hirop@ng-CPU03
   
   In this case, the user was specifically told that ``ng-CPU03`` is the node to use for their computations.

Jump Host Login Method
$$$$$$$$$$$$$$$$$$$$$$$$$

You can combine the secure and login node ``ssh`` commands into one by specifying the bastion host as a *jump* host. The jump host is used to connect to your destination node without needing to execute the ``ssh`` command twice. 

.. code-block:: terminal

   ssh -J <your_username>@ngale-bastion-1.ncsa.illinois.edu <your_username>@ng-<login_node>

For example, user ``test1`` can log in to the Nightingale login node ``astro07`` without logging in to the bastion host first with the following ``ssh`` command:
   
.. code-block:: terminal

   ssh -J test1@ngale-bastion-1.ncsa.illinois.edu test1@ng-astro07

Command-line SSH Clients
--------------------------

SSH is a client-server architecture that provides a secure channel over an unsecured network. An SSH client is a program for securely logging in to and executing commands on a remote machine. SSH encrypts the data sent over an open network, such as the internet, so that it can't be read by others.

Several SSH-based clients are available for accessing Nightingale. The client you use will depend on your workstation’s operating system.

Microsoft Windows
~~~~~~~~~~~~~~~~~~~

You can use the built-in SSH Client in Windows (version 10 and later) or select from several freely available third-party SSH clients. 
These typically provide a graphical user interface (GUI) rather than a command-line interface. `PuTTY <http://www.chiark.greenend.org.uk/~sgtatham/putty/>`_ is a popular choice; `MobaXterm <http://mobaxterm.mobatek.net/>`_ is another one.

Mac OS X
~~~~~~~~~

Mac OS X comes with a built-in open-source version of SSH called OpenSSH; access it via the Terminal application. 
`PuTTY <http://www.chiark.greenend.org.uk/~sgtatham/putty/>`_ is also available for Mac OS X.

Linux
~~~~~~~

The Linux operating system has SSH built into it, use the Linux terminal application to connect via SSH. 
`PuTTY <http://www.chiark.greenend.org.uk/~sgtatham/putty/>`_ is also available for Linux.

.. _access_vpn:

Accessing Nightingale using a VPN
-----------------------------------

If you log in to Nightingale from the University of Illinois campus, you don't need to use a Virtual Private Network (VPN). To access Nightingale from off campus, you will need to set up and activate a VPN first. A VPN sends your network traffic over an encrypted channel to a server on a different network, making your traffic originate within that other network. In this case, traffic will effectively originate inside of the University of Illinois, which adds an additional level of security and protection for your connection.  

There are two VPN services that will allow you to log in to Nightingale from off campus. The first is the University of Illinois VPN, which members of UIUC campus should use by default. The other is the NCSA VPN, which is available for Nightingale users not associated directly with UIUC. 

If you have trouble setting up or using either of these VPNs, or have questions, please :ref:`submit a support request <help>`.  

.. note::

   If your login freezes when you try to log in to Nightingale, this may be your problem.  Please try one of these VPN methods.  

University of Illinois VPN
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If you are a member of the University of Illinois, you can use the `University of Illinois VPN service <https://answers.uillinois.edu/illinois/98773>`_.  You will need to authenticate to the VPN service itself using your University NetID, password, and two-factor authentication (2FA).  

NCSA VPN
~~~~~~~~~

If you don't have a University of Illinois NetID, you will need to use the `NCSA VPN <https://wiki.ncsa.illinois.edu/display/NetEng/Virtual+Private+Network+%28VPN%29+Service>`_.  

Connecting with Terminal, SSH, and XQuartz (for users connecting from Mac OS machines)
----------------------------------------------------------------------------------------

One-time X Window Software Install
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If you want to use an application from Nightingale and have its windows on your own computer, before logging in, install XQuartz on your Mac OS system. You can `download XQuartz here <https://www.xquartz.org/>`_. Most Nightingale users will want to do this.  

One-time SSH Configuration 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Open the **Terminal** application on your Mac. 

#. Enter the following command into the terminal:

   .. code-block:: terminal

      cd ~/.ssh 

#. Enter the following command into the terminal:

   .. code-block:: terminal

      nano config

   This will bring you into an editor program that looks like this:

   .. code-block:: terminal

       UW PICO 5.09                            File: config                               







       ^G Get Help   ^O WriteOut   ^R Read File  ^Y Prev Pg    ^K Cut Text   ^C Cur Pos    
       ^X Exit       ^J Justify    ^W Where is   ^V Next Pg    ^U UnCut Text ^T To Spell   

   The editor allows you to edit a configuration file that sets up connections to the outside world, so you don't have to type as much all the time. 

#. Copy and paste the following configuration file code block into your terminal. Before you run it, you will modify the code in the next steps. 

   .. code-block:: terminal

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

#. Use the arrow keys to position your cursor and make the following modifications:

   a. Replace ``YOUR_USERNAME`` with your NCSA identity username. 

   b. If you have an interactive node assigned to you, you can add another copy of the last stanza of the configuration file; in that stanza, replace ``ng-login01`` with the name of your login node.  

   For example, a user with username ``hirop`` and the assigned node ``ng-gpu-x07`` would have the following configuration file:  

   .. code-block:: terminal

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
      
#. After you finish modifying the file, press **Control+O** to write the file.

#. Press **return** (or **Enter**) to confirm the file name. 

#. Press **Control+X** to exit the editor and you are back at the prompt.  
      
Logging in to Nightingale
~~~~~~~~~~~~~~~~~~~~~~~~~~
      
After the preceding one-time steps are complete, follow these steps each time you want to log in to Nightingale:

#. Enter the following into the terminal (if you are logging in to an interactive node, replace ``ng-login01`` with the name of that interactive node):

   .. code-block:: terminal

      ssh -X ng-login01

   If you see a message that begins "The authenticity of host...." and ends with "Are you sure you want to continue connecting (yes/no/[fingerprint])?", enter ``yes``.  

#. Enter your NCSA (Kerberos) password at the prompt. Note, the terminal will not show your password (or placeholder symbols such as asterisks [*]) as you type.  

#. There will be a Duo prompt asking for a passcode or for "option 1". You may either:

   - Enter ``1`` and approve the Duo push notification on your phone.
   
   Or 

   - Enter a 6-digit passcode from the **NCSA** entry of your Duo app.  

#. Again, enter your NCSA (Kerberos) password at the prompt. Note, the terminal will not show your password (or placeholder symbols such as asterisks [*]) as you type.  

#. You should have a prompt that reflects that you are on a Nightingale node. It will include ``@ng-`` and look similar to this example for user ``hirop`` on node ``ng-gpu-m01``: 

   .. code-block:: terminal

      [hirop@ng-gpu-m01 ~] $

   You can load modules, run software, and access your files from here.  

Connecting with MobaXterm (for users connecting from Windows machines)
------------------------------------------------------------------------

You can install `MobaXterm <https://mobaxterm.mobatek.net/>`_ on your workstation and use it to connect to Nightingale nodes using SSH. 
MobaXterm enables an SSH connection and provides other useful utilities you can use when communicating with a cluster, such as file transfer and editing.

Use the following steps to install MobaXterm and connect to Nightingale. Nightingale has extra security to protect the data stored on it, so configuring this connection is slightly more complicated than other HPC clusters. The difference involves adding the SSH connection to the secure bastion node; this is described in Steps 5 and 6 of the one-time setup instructions.

One-time setup
~~~~~~~~~~~~~~~ 

#. `Download MobaXterm <https://mobaxterm.mobatek.net/download-home-edition.html>`_ and install it on your Windows workstation. 

   You can install either the Portable or Installer edition of MobaXterm. You will need to have admin privileges to install the Installer edition. 
   The Portable edition does not require admin privileges, to use it **extract** the downloaded zip file and click **mobaxterm.exe**.

#. Launch the MobaXterm application and click **Session** in the upper left of the window to start an SSH session.

   .. figure:: images/accessing/mobaxterm-terminal-session.png
      :alt: MobaXterm initial window with Session button circled.
      :width: 150

#. Select **SSH** from the session types and click **OK**. 

   .. figure:: images/accessing/mobaxterm-session-ssh.png
      :alt: MobaXterm Session window with SSH button circled.
      :width: 600

#. In the **Basic SSH Settings** tab:

   a. In the **Remote host** box, enter the name of the login node you want to access (either a general access or interactive node).

   b. Select the **Specify username** checkbox and enter your NCSA Identity username.

   .. figure:: images/accessing/mobaxterm-basic-ssh-username.png
      :alt: MobaXterm Session window with Basic SSH Settings filled in.
      :width: 750

#. In the **Network settings** tab, click **SSH gateway (jump host)**.

   .. figure:: images/accessing/mobaxterm-network-settings.png
      :alt: MobaXterm Session window with showing Network settings tab clicked and SSH gateway jump host button highlighted.
      :width: 750

#. In the **jump hosts configuration** window:

   a. In the **Gateway host** box, enter ``ngale-bastion-1.ncsa.illinois.edu``. 

   b. In the **Username** box, enter your NCSA username. 

   c. Click **OK**. 

   You may see a warning message saying that your remote host identification has changed; click **Yes** to continue.

   .. figure:: images/accessing/mobaxterm-jump-host-config.png
      :alt: MobaXterm Session window with showing values for the SSH gateway jump host filled in.
      :width: 600

#. You should now be back in the **Session settings** window. Click **OK** to initiate your SSH connection. 

#. A terminal window will be displayed asking for your password; enter your NCSA (Kerberos) password and press **Enter**.

Logging in to Nightingale
~~~~~~~~~~~~~~~~~~~~~~~~~~

After the preceding one-time steps are complete, follow these steps each time you want to log in to Nightingale:

#. Open **MobaXterm**. 

#. In the left bar, there is a list of **User sessions**, each one is a node that you have configured for logging in. 

   Right-click on the Nightingale node you want to log in to and select **execute**. 

#. A window will pop up asking for your password. Enter your NCSA (Kerberos) password and press **Enter** or click **OK**.

#. A second window will pop up asking for your 2FA code. 

   a. On your phone, open the **Duo app**.

   b. Select the **NCSA** entry (not the *University of Illinois* entry).

   c. Enter the 6-digit passcode displayed in the Duo app into the pop-up window.  

#. A black window without a prompt will appear. **You may need to wait 30 seconds or a minute here.** 

   When it asks for your password, enter your NCSA (Kerberos) password. Note, the window will not show your password (or placeholder symbols such as asterisks [*]) as you type.

#. You are now ready to work. You should have a prompt at the bottom and a file window on the left showing your directories on Nightingale.  

Account Administration
------------------------

After you have a project group set up on Nightingale, there is an approval process to add new users to the system. To start the process, :ref:`submit a support request <help>`.

Other account and project administration tasks, such as resetting your password, are managed by the NCSA Identity and Group Management tools. 
See the `NCSA Allocation and Account Management documentation page <https://wiki.ncsa.illinois.edu/display/USSPPRT/NCSA+Allocation+and+Account+Management>`_ for more information.

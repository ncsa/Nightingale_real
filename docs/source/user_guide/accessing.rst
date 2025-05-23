.. _access:

Login Methods
================

After you have an :ref:`account on Nightingale <allocations>`, log in to the system using an Secure Shell (SSH) client on your local desktop or laptop. 
Because of the added security for Nightingale, you will first log in to Nightingale's secure node and then log in to a general access login node or, for groups that have them, a specialized interactive node.

.. _node_hostnames:

Node Hostnames
----------------

Secure Node Hostname
~~~~~~~~~~~~~~~~~~~~~

.. code-block:: terminal

   ngale-bastion-1.ncsa.illinois.edu 

General Access Login Nodes Hostnames
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: terminal

   ng-login01.ngale.internal.ncsa.edu
   ng-login02.ngale.internal.ncsa.edu

Specialized Interactive Node Hostname
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: terminal

   NODENAME.ngale.internal.ncsa.edu

``NODENAME`` will be something of the form ``ng-ai22``, ``ng-gpu-h35``, or ``ng-gpu-m37``. 

.. note::

   - Your PI can tell you if your allocation has a specialized interactive node and if so, its hostname.
   - All Nightingale users have access to the general access login nodes (ng-login01 and ng-login02). These nodes are a shared resource for all system users, limit your use of them to editing, compiling, and building your programs.

General Login Process
------------------------

To log in to Nightingale, establish an SSH connection to the secure node and then establish an SSH connection to your login or interactive node. These are the steps:

#. ``ssh`` to the secure node ``ngale-bastion-1.ncsa.illinois.edu``. (Replace ``<your_username>`` with your NCSA identity username.)
   
   .. code-block:: terminal

      ssh <your_username>@ngale-bastion-1.ncsa.illinois.edu

#. Enter your NCSA (Kerberos) password. Note, the terminal will *not* show your password (or placeholder symbols such as asterisks [*]) as you type.
#. Enter ``1`` to send a push to the Duo app on your phone.
#. Approve the push request on your phone.

   After you approve the push, you will be at a prompt on the ``ngale-bastion-1`` node that will look similar to:
   
   .. code-block:: terminal

      [<your_username>@ngale-bastion-1 ~]$

#. ``ssh`` to your login or interactive node using the appropriate :ref:`hostname <node_hostnames>`, following this syntax:
   
   .. code-block:: terminal

      ssh <your_username>@ng-<node_name>

   For example, this is the command for a user with the username ``hirop`` and the node name ``CPU03``:
   
   .. code-block:: terminal

      ssh hirop@ng-CPU03

.. note::

   - Connecting to Nightingale using the vscode program is not currently supported by the system.

Jump Host Login Method
~~~~~~~~~~~~~~~~~~~~~~~~

You can combine the secure and login node ``ssh`` commands into one by specifying the secure node as a *jump host*. The jump host is used to connect to your destination node without needing to execute the ``ssh`` command twice. 

.. code-block:: terminal

   ssh -J <your_username>@ngale-bastion-1.ncsa.illinois.edu <your_username>@ng-<login_node>

For example, user ``test1`` can log in to the Nightingale login node ``astro07`` with the following command:
   
.. code-block:: terminal

   ssh -J test1@ngale-bastion-1.ncsa.illinois.edu test1@ng-astro07

After you enter the ``ssh`` command:

#. Enter your NCSA (Kerberos) password, when prompted.
#. Approve the NCSA Duo push notification on your phone.
#. Again, enter your NCSA (Kerberos) password, when prompted.

Command-line SSH Clients
--------------------------

SSH is a client-server architecture that provides a secure channel over an unsecured network. An SSH client is a program for securely logging in to and executing commands on a remote machine. SSH encrypts the data sent over an open network, such as the internet, so that it can't be read by others.

Several SSH clients are available for accessing Nightingale. The client you use will depend on your workstation’s operating system.

Microsoft Windows
~~~~~~~~~~~~~~~~~~~

You can use the built-in SSH Client in Windows (version 10 and later) or select from several freely available third-party SSH clients. 
Third-party clients typically provide a graphical user interface (GUI) rather than a command-line interface. `PuTTY <http://www.chiark.greenend.org.uk/~sgtatham/putty/>`_ is a popular choice; `MobaXterm <http://mobaxterm.mobatek.net/>`_ is another one.

Mac OS X
~~~~~~~~~

Mac OS X comes with a built-in open-source version of SSH called OpenSSH; access it via the Terminal application. 
`PuTTY <http://www.chiark.greenend.org.uk/~sgtatham/putty/>`_ is also available for Mac OS X.

Linux
~~~~~~~

Linux has SSH built into it, use the Linux terminal application to connect via SSH. 
`PuTTY <http://www.chiark.greenend.org.uk/~sgtatham/putty/>`_ is also available for Linux.

X Window Servers
-------------------

Originally developed for Unix, the X Window System allows a program on one computer to open windows on another computer’s screen (usually your desktop/laptop). 
The program that runs on the Nightingale is called the *client*. 
The program that runs on your desktop/laptop computer is called the *server*. 
X Window servers are available for Microsoft Windows, Mac, and Unix/Linux.

One-Time Setup
~~~~~~~~~~~~~~~

Before logging in to Nightingale, complete these one-time steps to set up the connection.

.. tabs::

   .. group-tab:: XQuartz (Mac OS)

      XQuartz allows you to use an application from Nightingale and have its windows on your own computer.

      #. `Download and install XQuartz <https://www.xquartz.org/>`_.
      
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
            
         This editor allows you to edit a configuration file that sets up connections to the outside world, so you don't have to type as much all the time. 
            
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
            
         b. If you have an interactive node assigned to you, you can add second copy of the last stanza of the configuration file; in that stanza, replace ``ng-login01`` with the name of your interactive node.  
            
         For example, a user with username ``hirop`` and the assigned interactive node ``ng-gpu-x07`` would have the following configuration file:  
            
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

   .. group-tab:: MobaXterm (Microsoft Windows)

      MobaXterm enables an SSH connection and provides other useful utilities, such as file transfer and editing.

      #. `Download and install MobaXterm <https://mobaxterm.mobatek.net/download-home-edition.html>`_. 
      
         You can install either the Portable or Installer edition of MobaXterm. You will need to have admin privileges on your machine to install the Installer edition. 
         The Portable edition does not require admin privileges, to use it **extract** the downloaded zip file and click **mobaxterm.exe**.
            
      #. Launch the MobaXterm application and click **Session** in the upper left to start an SSH session.
            
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
            
         b. In the **Username** box, enter your NCSA identity username. 
            
         c. Click **OK**. 
            
         You may see a warning message saying that your remote host identification has changed; click **Yes** to continue.
            
         .. figure:: images/accessing/mobaxterm-jump-host-config.png
            :alt: MobaXterm Session window with showing values for the SSH gateway jump host filled in.
            :width: 600
            
      #. You should now be back in the **Session settings** window. Click **OK** to initiate your SSH connection. 
            
      #. A terminal window will be displayed asking for your password; enter your NCSA (Kerberos) password and press **Enter**.
      
Log in to Nightingale 
~~~~~~~~~~~~~~~~~~~~~~~

After the preceding one-time setup is complete, follow these steps each time you want to log in to Nightingale.

.. tabs::

   .. group-tab:: XQuartz (Mac OS)

      #. Enter the following into the terminal (if you are logging in to an interactive node, replace ``ng-login01`` with the name of that interactive node):
      
         .. code-block:: terminal
            
            ssh -X ng-login01
            
         If you see a message that begins "The authenticity of host...." and ends with "Are you sure you want to continue connecting (yes/no/[fingerprint])?", enter ``yes``.  
            
      #. Enter your NCSA (Kerberos) password at the prompt. Note, the terminal will *not* show your password (or placeholder symbols such as asterisks [*]) as you type.  
            
      #. There will be a Duo prompt asking for a passcode or for "option 1". You may either:
            
         - Enter ``1`` and approve the Duo push notification on your phone.
               
         Or 
            
         - Enter a 6-digit passcode from the **NCSA** entry of your Duo app.  
            
      #. Again, enter your NCSA (Kerberos) password at the prompt. Note, the terminal will *not* show your password (or placeholder symbols such as asterisks [*]) as you type.  
            
      #. You should have a prompt that reflects that you are on a Nightingale node. It will include ``@ng-`` and look similar to this example for user ``hirop`` on node ``ng-gpu-m01``: 
            
         .. code-block:: terminal
            
            [hirop@ng-gpu-m01 ~] $
           
         You can load modules, run software, and access your files from here.  

   .. group-tab:: MobaXterm (Microsoft Windows)

      #. Open **MobaXterm**. 
      
      #. In the left bar, there is a list of **User sessions**, each one is a node that you have configured for logging in. 
            
         Right-click on the Nightingale node you want to log in to and select **execute**. 
            
      #. A window will pop up asking for your password. Enter your NCSA (Kerberos) password and press **Enter** or click **OK**.
            
      #. A second window will pop up asking for your 2FA code. 
            
         a. On your phone, open the **Duo app**.
            
         b. Select the **NCSA** entry (not the *University of Illinois* entry).
            
         c. Enter the 6-digit passcode displayed in the Duo app into the pop-up window.  
            
      #. A black window without a prompt will appear. **You may need to wait 30 seconds or a minute here.** 
            
         When it asks for your password, enter your NCSA (Kerberos) password. Note, the window will *not* show your password (or placeholder symbols such as asterisks [*]) as you type.
            
      #. You are now ready to work. You should have a prompt at the bottom and a file window on the left showing your directories on Nightingale.  

|

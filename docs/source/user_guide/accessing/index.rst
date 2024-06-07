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

#. If you are not on campus, connect to the University of Illinois VPN or NCSA VPN (see :ref:`access_vpn`).
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

Jump Host Login Method
~~~~~~~~~~~~~~~~~~~~~~~~

You can combine the secure and login node ``ssh`` commands into one by specifying the secure node as a *jump host*. The jump host is used to connect to your destination node without needing to execute the ``ssh`` command twice. 

.. code-block:: terminal

   ssh -J <your_username>@ngale-bastion-1.ncsa.illinois.edu <your_username>@ng-<login_node>

For example, user ``test1`` can log in to the Nightingale login node ``astro07`` with the following command:
   
.. code-block:: terminal

   ssh -J test1@ngale-bastion-1.ncsa.illinois.edu test1@ng-astro07

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

.. _access_vpn:

Access Nightingale using a VPN
-----------------------------------

.. note::

   If your login freezes when you try to log in to Nightingale, this may be your problem. Please try one of these VPN methods.  

To access Nightingale off campus, you first need to set up and activate either the University of Illinois VPN or the NCSA VPN.

If you log in to Nightingale from the University of Illinois campus, you don't need to use a VPN. 

University of Illinois VPN
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If you are a member of the University of Illinois, you can use the `University of Illinois VPN service <https://answers.uillinois.edu/illinois/98773>`_.  You will authenticate to the VPN service itself using your University NetID, password, and two-factor authentication (2FA).  

NCSA VPN
~~~~~~~~~

If you don't have a University of Illinois NetID, you will need to use the `NCSA VPN <https://wiki.ncsa.illinois.edu/display/NetEng/Virtual+Private+Network+%28VPN%29+Service>`_.  

X Window Servers
-------------------

Originally developed for UNIX, the X Window System allows a program on one computer to open windows on another computer’s screen (usually your desktop/laptop computer). 
The program that runs on the Nightingale is called the *client*. 
The program that runs on your desktop computer is called the *server*. 
X Window servers are available for Microsoft Windows, Apple Mac, and UNIX/Linux.

.. toctree::
   :maxdepth: 1

   xquartz
   mobaxterm  

|

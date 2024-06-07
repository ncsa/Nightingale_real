Connect with Terminal, SSH, and XQuartz (for Mac OS)
======================================================

XQuartz allows you to use an application from Nightingale and have its windows on your own computer. Use the following steps to set up XQuartz and connect to Nightingale.

.. _one-time-xquartz:

One-time Setup
-----------------

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

.. _xquartz-log-in:
            
Log in to Nightingale
------------------------
            
After the preceding one-time steps are complete, follow these steps each time you want to log in to Nightingale:
      
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

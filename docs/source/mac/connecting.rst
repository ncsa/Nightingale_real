#######################################################################################
Connecting with Terminal, ssh, and XQuartz (for users connecting from Mac OS machines)
#######################################################################################

One-time X-windows Software Install
=======================================

If you want to use an application from Nightingale and have its windows on your own computer, before logging in, install XQuartz on your Mac OS system.  You can `download it here <https://www.xquartz.org/>`_.  Most users of Nightingale will want to do this.  

One-time Ssh Configuration 
==============================

Open the "Terminal" application on your mac.  That presents a black window to you that you can type commands into.  At the prompt, type "cd ~/.ssh" and then "return" or "enter" (in these instructions, "return" and "enter" are interchangable).  

Type "nano config" and hit return.  This will bring you into an editor program that looks like this:

::  

    UW PICO 5.09                            File: config                               







    ^G Get Help   ^O WriteOut   ^R Read File  ^Y Prev Pg    ^K Cut Text   ^C Cur Pos    
    ^X Exit       ^J Justify    ^W Where is   ^V Next Pg    ^U UnCut Text ^T To Spell   

This allows you to edit a configuration file that sets up connections to the outside world so you don't have to type as much all the time.  Cut the lines out of the following box, and then modify them in your window according to the instructions below the box. 

::

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


After pasting those lines into the file (using the arrow keys to position your cursor) edit where it says "YOUR_USERNAME" and replace it with your NCSA identity username.  Also, if you have an interactive node assigned to you, you can add another copy of the last stanza of the configuration file, and in that stanza, replace "ng-login01" with the name of *your* login node.  

So for example, a user with username "hirop" who was assigned node ng-gpu-x07 would have a configuration file something like the following.  


::

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
      
Once you have finished editing the file, it *Control*-o to write the file.  Hit enter to confirm the file name.  Then hit *Control*-x to exit the editor, and you're back at the prompt.  
      
Log Into Nightingale
============================
      
The above are one-time instructions to set up your computer for working on Nightingale.  To log into Nightingale to begin work, type the following at the prompt:

ssh -X ng-login01

(If you're logging into an interactive node, replace "ng-login01" with the name of that active node.)

You may see a message that begins "The authenticity of host...." and ends with "Are you sure you want to continue connecting (yes/no/[fingerprint])?".  You may safely type Y-E-S then enter.  

You'll be asked for a password.  Enter your NCSA (kerberos) password.  You **will not see your characters** echoed back to the screen; just type it blindly.  

Then you'll see a duo prompt asing for a passcode or for "option 1".  You may either type "1", then your phone Duo will ask you for login confirmation.  Or instead of 1, you may enter a 6-digit password from the **NCSA** entry of your Duo app.  

Then you'll be asked for your password again; that's again your NCSA password.  You again will not see it echoed to the screen; just type it blindly.  

You should now be at a propmt that reflects that you are on a Nightingale node.  You can load modules and run software and access your files from there.  

#########################################################################
Connecting with MobaXterm (for users connecting from Windows machines)
#########################################################################

You can install `MobaXterm <https://mobaxterm.mobatek.net/>`_ on your 
workstation and use it to connect to Nightingale node using SSH. MobaXterm 
enables an SSH connection and provides other useful utilities you can use 
when communicating with a cluster, such as file transfer and editing.

Follow the steps below to install MobaXterm and connect to Nightingale. (Nightingale has extra security to protect the data stored on it, so configuring this connection is slightly more complicated than other HPC clusters. The difference involves adding the SSH connection to the secure bastion node. How to do this is described in Step 6 and 7.)

One-time setup
===================

This section is the one-time setup on your Windows machine so that it can connect to Nightingale.  

**Step 1.** `Download MobaXterm <https://mobaxterm.mobatek.net/download-home-edition.html>`_ and install it on your Windows workstation. 

You can install either the Portable or Installer edition of MobaXterm. You will need to have admin privileges to install the Installer edition. The Portable edition does not require admin privileges and to use it just extract the downloaded zip file and click mobaxterm.exe.

**Step 2.** Launch the MobaXterm application and click the 'Session' button in the upper left of the window to start an SSH session.

..  image:: ../../user_guide/images/accessing/ng_mxt_session_button.gif
  :alt: MobaXterm initial window with Session button circled.


**Step 3.** Select 'SSH' from the session types displayed and click the 'OK' button. 

..  image:: ../../user_guide/images/accessing/XC_01_select_ssh.png
    :alt: MobaXterm Session window with SSH button circled.


**Step 4.** You will now see an area titled 'Basic SSH Settings.' 

..  image:: ../../user_guide/images/accessing/XC_specify_host_username.png
  :alt: MobaXterm Session window with Basic SSH Settings area displayed.



**Step 5.** In the remote host text box, enter the name of the login node you want to access (either a general access or interactive node). Then check the box 'Specify username' and enter your NCSA Identity username as shown in the following example. 

..  image:: ../../user_guide/images/accessing/XC_specify_host_username2.png
  :alt: MobaXterm Session window with Basic SSH Settings filled-in.

**Step 6.** Next, click the "Network settings" tab and then click the "SSH gateway (jump host)" button.

..  image:: ../../user_guide/images/accessing/XC_network_settings.png
  :alt: MobaXterm Session window with showing Network settings tab clicked and SSH gateway jump host button displayed.

**Step 7.** In the configuration window displayed, enter 
"ngale-bastion-1.ncsa.illinois.edu" in the "Gateway host" box and your NCSA username in the "Username" box. Then click the 'OK' button. (You may see a warning message saying that your remote host identification has changed. Go ahead and click the Yes button to continue.)

..  image:: ../../user_guide/images/accessing/XC_jump_host_filled_in.png
  :alt: MobaXterm Session window with showing values for the SSH gateway jump host filled-in.

**Step 8.** You should now be back in the Session settings window. Click the 'OK' button to initiate your SSH connection. A terminal window will be displayed asking for your password. Enter your password and press return.

Logging Into Nightingale
===========================

Once the above steps are complete, here's what you do each time you want to log into Nightingale to work.

Open up MobaXterm.  In the left bar, there's a list of "user sessions".  Each one is a node that you configured above for logging in.  Mouse over the Nightingale node you want to log into, right click, and in the resulting menu, select "execute". 

A window will pop up, asking for your password.  This is your NCSA password.  As you type it, you will see a row of "*********".  Hit enter or click "OK".

A second window will pop up asking for your 2FA code.  Open your Duo app, click on the "NCSA" entry (not the "University of Illinois" entry) and type the 6-digit code you see into the window.  As the password above, you will see it as ******.  

Then the screen will bring up a black window but without a prompt.  You may need to wait 30 seconds or a minute here.  Then it will ask you for your password.  You will type your NCSA password again.  **It will not echo the characters back; you must type it blind**.  

Then you should have a prompt at the bottom, and a file window on the left showing your directories on Nightingale, and you're ready to work.  

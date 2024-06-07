Connect with MobaXterm (for Microsoft Windows)
================================================
 
MobaXterm enables an SSH connection and provides other useful utilities, such as file transfer and editing.

Use the following steps to set up MobaXterm and connect to Nightingale. Nightingale has extra security to protect the data stored on it, so configuring this connection is slightly different than other HPC clusters. The difference involves adding the SSH connection to the secure node; this is described in Steps 5 and 6 of the one-time setup instructions.
      
One-time Setup
----------------
      
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
-----------------------
      
After the preceding one-time setup is complete, follow these steps each time you want to log in to Nightingale:
      
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

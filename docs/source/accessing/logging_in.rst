########################
Logging Onto Nightingale
########################

Once you have obtained an account on Nightingale, you can log on using an SSH (Secure Shell) client on your local desktop or laptop. 
Because of the added security for Nightingale, you will first log onto Nightingale's secure node and then log onto a general access login node 
or, for groups that have them, a specialized interactive node. The hostnames for these login nodes are listed below.

**Secure Node Hostname**::

   ngale-bastion-1.ncsa.illinois.edu 

**General Access Login Nodes Hostnames**::

   ng-login01.ngale.internal.ncsa.edu
   ng-login02.ngale.internal.ncsa.edu

**Specialized Interactive Node Hostname**::

   <ng-yourgroup01>.ngale.internal.ncsa.edu

where <ng-yourgroup01> is the name of your allocation group. 

**Notes:** 

- Your group manager can inform you if your allocation has a Specialized Interactive node and its hostname.
- All Nightingale users have access to the general access login nodes. Please be aware that these nodes are a shared resource for all 
  system users, and you should limit your use of them to editing, compiling, and building your programs.

**General Log in Process**

You can log onto Nightingale by following these steps:

1. If not on campus, connect to the campus VPN. (`Instructions for installing the campus VPN <https://answers.uillinois.edu/illinois/98773>`_)
2. SSH to the secure node ngale-bastion-1.ncsa.illinois.edu.
3. Enter your NCSA username and password.
4. Enter '1' to send a push to the Duo app on your smartphone.
5. Approve the request on your phone.
6. SSH to your login node using the appropriate hostname (see above).

Below is a sample SSH command line to log into Nightingale's secure node where <username> is the username you created for your NCSA identity.::

   ssh <username>@ngale-bastion-1.ncsa.illinois.edu

After entering the ssh command, you will be prompted to enter your password, followed by a prompt to send a push to the Duo app. After you have approved the push, you may enter the SSH command using the hostname of your login node.

**Passwords**

When typing passwords into terminals, you *will not see you characters*.  That is, you will type your password, and type "1" to send the push to your phone, and you won't see anything on the screen.  This is normal.  You just need to type blindly, and then hit "enter" or "return" to complete the entry. 

Also, when setting up your NCSA ID ("kerberos") password, please use a password that you can easily type with your keyboard.  We have discovered that cutting and pasting passwords from a password manager (or document on your own computer?) is a very error-prone process and produces very inconsistent results and it seems like your password is wrong.  If you can type it with the keyboard, results are much more consistent, so we strongly encourage you to set a password that you can type.

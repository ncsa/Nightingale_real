Accessing the System and Account Administration
============================================================

The page contains information about how to set up your machine to log
into and use the Nightingale cluster computer at NCSA. This page will
contain general setup instructions for logging into your interactive
node on the Nightingale cluster.

**If you are new to Linux OS, here is a page to walk Windows users to set up your computer to log in.**

If you can't find information to help you in this user guide (try searching in the top left search box) please don't hesitate to `submit a help ticket <./help.html>`_ to ask your question.  

Introduction to Nightingale
-------------------------------

Nightingale is a cluster computer running a Linux OS. That is, it is several separate
computers (called "node"s) connected together by network that share user account information
and file systems. 
When you log into Nightingale, you will typically log into a
particular node that depends on the type of allocation your 
group has.  Please see the "Nightingale Nodes" section above for specifics.  

Logging onto Nightingale
~~~~~~~~~~~~~~~~~~~~~~~~

To work on Nightingale, you will "log in" to it. Logging in establishes
a connection between your computer and a node of Nightingale, so that
you can use software on Nightingale to manipulate and analyze data on
Nightingale. To log into Nightingale, user will need at least a ssh client
available on their local desktop or laptop to make the connection. All
Nightengale users must use a ssh based connection to go through the
secure node (`bastion
host <https://en.wikipedia.org/wiki/Bastion_host>`__) to be able to
login to the general access head (login) nodes or, for groups that have
them, their specific interactive specialized nodes.

| 

+----------+-----------------------------------+---------------------------------------+
| Access   | Secure Node                       | General Access Head Nodes             |
| Method   |                                   |                                       |
+----------+-----------------------------------+---------------------------------------+
| SSH      | ngale-bastion-1.ncsa.illinois.edu | ng-login01.ngale.internal.ncsa.edu    |
+----------+-----------------------------------+---------------------------------------+
|          |                                   | ng-login02.ngale.internal.ncsa.edu    |
+----------+-----------------------------------+---------------------------------------+

**Note:** All Nightingale users have access to the general access login
nodes. Please be aware that the general access head nodes are a shared
resource for all users of the system and their use should be limited to
editing, compiling and building your programs.

| 

+----------+-----------------------------------+--------------------------------------------+
| Access   | Secure Node                       | General Access Login Nodes                 |
| Method   |                                   |                                            |
+----------+-----------------------------------+--------------------------------------------+
| SSH      | ngale-bastion-1.ncsa.illinois.edu | ng-group_node.ngale.internal.ncsa.edu      |
+----------+-----------------------------------+--------------------------------------------+


**Note:** Certain Nightingale groups have exclusive access to their
interactive specialized nodes.

Mac OS users
~~~~~~~~~~~~~~

You will log into Nightingale using the "ssh" command in your Terminal
program. It's already installed and ready. You will also need an
application that serves as an "X-windows server". For Mac OS users, we
recommend XQuartz.

Unix/Linux OS users
~~~~~~~~~~~~~~~~~~~~~

Will also log into Nightingale using the "ssh" client that is run from
the command line in the terminal. Generally, the "ssh" client along with
an "X-Windows" server should be available by default on recent versions
of Unix/Linux OSes.

Windows users
~~~~~~~~~~~~~~

We recommend Nightingale users first install a program called MobaXterm
on their computers and then use that to log into Nightingale. This
install process is detailed on this separate page.



Accessing the System for Windows Users (Moba Xterm)
====================================================

Introduction for Windows Nightingale users:
---------------------------------------------

Nightingale is a Linux-based cluster computer. That means users used to
only using Windows computers, there will be a lot of things to learn.
This page is for those people. These instructions will walk you through
setting up your own computer so that you can log into Nightingale and do
your work. These instructions are admittedly complicated but you only
have to do this once. Before starting these instructions, you should
already have an NCSA identity (username), know your NCSA kerberos
password, and have Duo hooked up and working with an NCSA ID.  Please go back to
the parent page of this page and go through the "NCSA Identity" process,
then come back here once you have that.

Brief overview of Nightingale
--------------------------------

A "cluster" computer is many computers
connected together in a network such that they work together in some
cases but work separately in others. Nightingale is the name of the
cluster as a whole, the individual computers within it are called
"nodes" (from the mathematical term). Typical Nightingale users (you)
will log into (connect to) to a specific node of Nightingale where your
data and software are set up for you to use to do your work. You will
need one extra piece of software on your Windows computer, called "Moba
Xterm" to do this. (There are other pieces of software that can
accomplish this, but this is the simplest way we could find to get
Windows users set up the way they need to be.)

Install the Moba Xterm application
-------------------------------------

The Moba Xterm application runs on your computer and connects it to a
Nightingale node, and allows you to run software as if your screen,
mouse, and keyboard were attached directly to that node of Nightingale.
The Nightingale cluster has extra security to protect the data on it, so
configuring this connection is slightly more complicated than some other
connections. The good news is, once you have this set up, it's easy to
use.

You will need to have administrative privileges on your machine to
install Moba Xterm. If you don't have that, you will need to have
someone install Moba Xterm for you. They can follow these instructions.

| Download Moba Xterm from this page:
  https://mobaxterm.mobatek.net/download-home-edition.html
| The best version is the "previous stable version" that's
  non-"portable" version.  Click on that button to download the .zip file.
  Once you have it, right click on the zip file, click on option
  "extract all", and choose a location. Then open up that folder, which
  will contain two files, one of which is a .msi file which is a Windows
  installer file. Double-click on the msi file, which will launch the
  Windows install Wizard. You'll need to accept the terms of service.
  It's fine to keep hitting "next". Installing in the default location
  is fine. You will probably need to authorize "MobaXterm installer" to
  make changes to your device. Allow this.

When you start Moba Xterm for the first time, you may get a warning from
"Windows Defender Firewall" saying it has blocked access for the
application "xwin_mobax". Go ahead and click all the boxes and then
click the "Allow access" button. (Most applications work locally, so if
they're trying to reach out over the network, something fishy is going
on. The whole point of Moba Xterm is that it connects to another
computer over the network. That's how it works. Nothing fishy here.)

If necessary install and launch a VPN
---------------------------------------

For security reasons, Nightingale only accepts connections from
computers on the UIUC campus. If you're going to connect to Nightingale
from a computer on the UIUC network (in a campus office, for instance)
then you can skip this section.

If you need to access Nightingale from outside the campus network, you
need to use a piece of software called a "VPN" ("Virtual Private
Network") to make your connection to Nightingale come from inside the
campus network and protects that traffic from being spied on. We will
link to instructions on how to set up a campus VPN here in the future.
If you need to set up a VPN and there's no link here, please contact
Nightingale user support.

Know which nightingale node you want
----------------------------------------

As mentioned above, nightingale is made up of many different nodes.
Several of those are "interactive" nodes, which are set up for
particular groups of users to do their work. There will be software
installed and any setup specific to that group's (your) needs. If you're
ready to test logging into an interactive node, you will have been told
what the name of that node is. The name will come in two forms. One form
is the hostname, which is just a string of characters, like
"beatlesGPU02", and the fully-qualified hostname, like
"rollingstonesGPU02.ncsa.illinois.edu". The hostname might be a word
that pertains to your project, and might contain something like "GPU",
and often will contain a number. If you don't know what the hostname of
the Nightingale node that you need to log into, stop following these
instructions and go find out. You can find out from your PI (the person
who invited you to work on Nightingale), or failing that, talk to
Nightingale user support.

**Initial Moba Xterm test**
---------------------------

Before you use these instructions, make sure you know what hostname
within the Nightingale cluster you need to log into. This is explained
in the previous section.

Open up the Moba Xterm application. Click the button in the middle of
the main window called "Start Local Terminal" to open up a new
connection. You will have a colorful window that has a prompt at the
bottom that allows you to type commands. The last part of the prompt
will probably be something like "/home/mobaxterm". To test that
everything is working, please type the following, all on one line. While
you're typing, substitute the hostname of **your** nightingale node for
"XXXXX", and substitute **your** NCSA identity username for "UUUUU".

::

   ssh -J UUUUU@ngale-bastion-1.ncsa.illinois.edu UUUUU@XXXXX.ngale.internal.ncsa.edu
   

so with the proper substitutions, if fictional user Hiro P. were using
this method to log into (fictional) Nightingale node "beatlesGPU02",
they would type the following:

::

   ssh -J hirop@ngale-bastion-1.ncsa.illinois.edu hirop@beatlesGPU02.ngale.internal.ncsa.edu
   

The text will ask you for your password. Type in your NCSA kerberos
password (YOU WILL NOT SEE THE CHARACTERS AS YOU TYPE. JUST TYPE IT
BLINDLY). Then it will ask you for a Duo code. Type "1", hit return,
your Duo device (usually your phone) will notify you of the request,
approve the connection on your Duo device. Then it will ask you for your
password again. Type it again, and again you won't see the characters.

Then you will be back at a prompt, but unlike before, the prompt will be
to execute commands on a node of Nightingale (rather than your own
computer). If it worked, the prompt you see will look something like
this, with the name of the node you logged into displayed as part of the
prompt:

::

   [UUUUU@XXXXX ~]$ 
   
So if fictional user "Hiro P." logs into the same (fictional) node as
above, it would look like this:

::

   [hirop@beatlesGPU02 ~]$ 
   

If you see this, that means you can successfully log into your node on
Nightingale. However, now you need to test that you can bring an
application window from Nightingale to your machine. Type "xclock" and
then hit return. If it immediately complains about something like
"DISPLAY not set", then something's wrong. In around about 10 seconds or
so, a square window with a running analog clock should show up on your
desktop. (Check your window bar if you don't see it; sometimes it hides
behind other windows.)

If that worked, you're all set. You just need to type that ssh line from
above to log into Nightingale to work. To make logging in simpler, and
enable moving files to Nightingale, configure Moba Xterm per the
following section.

Configuring Moba Xterm
------------------------------

Once you know that logging in works, you should configure Moba Xterm as
follows.

Click on the "Session" button near the upper left of the Moba Xterm
window.

..  image:: ../../user_guide/images/accessing/ng_mxt_session_button.gif

This brings up a "Session settings" window. Click "SSH" in the very
upper left corner of that window.

..  image:: ../../user_guide/images/accessing/XC_01_select_ssh.png

This will populate the lower part of the window. Insert **the name of
your interactive node** into the "Remote host" blank. Click on "specifiy
username" as below. The username will have "<default"> in the blank, as
here:

..  image:: ../../user_guide/images/accessing/XC_specify_host_username.png

Replace <default> with your own username. This is what it looks like,
using my username "csteffen":

..  image:: ../../user_guide/images/accessing/XC_specify_host_username2.png

In the lower part of the window, click on the "Network settings" tab.
Once there, click "SSH gateway (jump host" in the middle.

..  image:: ../../user_guide/images/accessing/XC_network_settings.png

This will bring up yet another configuration window. Put
"ngale-bastion-1.ncsa.illinois.edu" in the "Gateway host" box (no matter
what Nightingale host you're logging into; all access goes through the
bastion host node: Put your NCSA username in the "Username" box.

..  image:: ./XC_jump_host_username.png

so that it looks like this:

..  image:: ../../user_guide/images/accessing/XC_jump_host_filled_in.png

Then click "Ok". Back in the Session settings, now click "OK" at the
bottom. This should open a new tab in your overall Moba Xterm window
that will log into your interactive node on Nightingale.

Moving files to Nightingale using Moba Xterm
------------------------------------------------

You may have files on your local system that you want to transfer to
Nightingale to use. These may be data files, or configuration program
files, or test files. Once you're logged in to Nightingale on Moba
Xterm, you can use Moba Xterm to transfer those files, just as if you
were copying them around your local machine.

Here, I'm starting with a test file on my local system:

..  image:: ./XF_original_file_in_folder.png

The file is called "testfile.pdf" and it's it' folder "source_folder" on
my desktop.

Then open up Moba Xterm, and log into your node on Nightingale. if
you've set up the login configuration correctly (see the configuration
section above) then the left part of your Moba Xterm winodow will be a
list of folders and files, and the pathname of the folder will end with
**your** Nightingale username (circled in red) and a slash "/", as
below. If you don't see this, then something is configured wrong and
you'll have to back up.

..  image:: ./XF_logged_in.png

It's often convenient to create a new folder if you're uploading files.
Click on the icon at the top of the left bar that's a folder with a
green "+" on it to create a new folder. Then you'll be asked to name it,
as below. I'm naming it "destination_folder".

..  image:: ./XF_create_destination_folder.png

Once you've created the destination folder, it will show up in the list
of folders. Here the folder I created is in the list.

..  image:: ./XF_destination_folder_exists.png

Double-click the folder you want to upload files into. Here I've
double-clicked the folder above ("destination_folder"). To make sure
you're in the right place, verify that the end of the pathname at the
top of the left window is the name of the folder where you want to be.
See the circled pathname here; it ends with "destination_folder".

..  image:: ./XF_in_destination_folder.png

Now position the two windows so you can see them both. Grab the file on
your system that you want to move, and drag it to the file area in the
Moba Xterm window. As you move the file over the Moba Xterm window, if
it's working, it will light up with "+ Copy". Drop it there, and Moba
Xterm will take care of copying the file to Nightingale.

..  image:: ./XF_drag_testfile.png

If everything works right, the (or files) will now exist on both
machines. You can now open the file, read it, and even modify it and
save it using software on Nightingale.

..  image:: ./XF_testfile_at_destination.png

Moving files from Nightingale to your local machine (downloading them; see warnings about this)
---------------------------------------------------------------------------------------------------

If you a file on Nightingale that you want to look at locally on your
own machine, you can download it, using essentially the reverse process
of uploading described above. Any files that you download **must**
legally clear to have on your machine; i.e. no identifying patient
information, etc. You would typically do this with summary statistics
data, but NOT original data.

You must be logged into Nightingale in the Moba Xterm application. If
you've set it up as on this page, on the left you'll see a file system
view of your directories on Nightingale. If you have a file that you've
exported on Nightingale, navigate to that file in the left window. You
can download it by right-clicking on it and selecting "copy", then going
to a directory on your own computer and right clicking and selecting
"paste". Or, you could drag the file from the Moba Xterm window onto a
directory folder that exists on your local computer. Either way, the
file will be copied.

| 

If you have questions: `SUBMIT A TICKET <./help.html>`_!
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

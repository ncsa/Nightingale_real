#######################################################################################
Connecting with Terminal, ssh, and XQuartz (for users connecting from Mac OS machines)
#######################################################################################

If you want to use an application from Nightingale and have its windows on your own computer, before logging in, install XQuartz on your Mac OS system.  You can `download it here <https://www.xquartz.org/>`_.  Most users of Nightingale will want to do this.  

Then open the "Terminal" application on your mac.  That presents a black window to you that you can type commands into.  At the prompt, type "cd ~/.ssh" and then "return" or "enter" (in these instructions, "return" and "enter" are interchangable).  

Then type "nano config" and hit return.  This will bring you into an editor program that looks like this:

..  

    UW PICO 5.09                            File: config                               







    ^G Get Help   ^O WriteOut   ^R Read File  ^Y Prev Pg    ^K Cut Text   ^C Cur Pos    
    ^X Exit       ^J Justify    ^W Where is   ^V Next Pg    ^U UnCut Text ^T To Spell   

This allows you to edit a configuration file that sets up connections to the outside world so you don't have to type as much all the time.  Cut the lines out of the following box, and then modify them in your window according to the instructions below the box. 

..

    Host ngb1
      HostName ngale-bastion-1.ncsa.illinois.edu
      ControlMaster auto
      ControlPath /tmp/ssh_mux_%h_%p_%r
      ControlPersist 5h
      User csteffen


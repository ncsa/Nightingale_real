##########################
Creating and Editing Files
##########################

Sometimes, it is easiest to create and edit your files directly on the cluster rather than transfer them back and forth. 
You can use various programs on clusters for working with plain text files. Examples include vi/vim, gedit, nano, and emacs. 
The vi/vim text editor is one of the most commonly used. However, if you are new to working in the Linux environment, 
the nano editor is recommended because it may be more similar to how you edit text files on a non-Linux-based machine. 
Several tutorials are available online if you want to know more about nano or vi. A couple of suggestions are listed below.

- `How-to-Geek: The Beginner’s Guide to Nano, the Linux Command-Line Text Editor <https://www.howtogeek.com/howto/42980/the-beginners-guide-to-nano-the-linux-command-line-text-editor/>`_

- `Wikibooks: Learning the vi Editor <https://upload.wikimedia.org/wikipedia/commons/d/d2/Learning_the_vi_Editor.pdf>`_ 

You can also edit files using MobaXterm's text editor. Brief instructions for using GNU nano and MobaXterm are given below.

GNU nano
--------

GNU nano is an easy-to-use command line text editor for Linux. To open an existing file or create a new one, type nano followed by the file name::

   nano file_name

This opens a new editor window in your terminal where you can start editing the file. At the bottom of the window, you will find a list of 
shortcuts to use with the nano editor. The caret symbol (^) represents the Ctrl key (e.g., to exit, type Ctrl+X). The letter M represents the 
Alt key (e.g., to undo type Alt+U).

MobaTextEditor
--------------

If you use MobaXterm to log into Nightingale, you will see a file browser in the left pane of the MobaXterm window.  Double-click on a selected 
file to open it in a separate window.  Please note that a temporary copy of files will be saved on your local machine when you use MobaTextEditor.  
The temporary files are saved in the AppData\Roaming folder on Windows and will be removed when you fully close MobaXterm on your machine.

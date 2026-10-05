# ftp server

Ftp another machine. It is also ncftp which adds extra features and grep for GUI ().Ftp is good
copy files to/from remote. Try "anonymous" if you don't have an account on the
remote server. After connection, use "? to see the list of available ftp commands. The essential ftp
command are: ls (see the files on the remote system), ASCII,binary (set the file transfer mode
either text or binary, important to select the proper one), get (copy a file from the remote system
to local), mget (get many files at once), put (copy a file from the local system to the
remote), mput (put many files at once, disconnect). For a script, you may want to
 use ncftp and ncftpget, for example:
ncftp -u my_user_name -p my_password -a remote.domain
remote_dir -a

# minicom

Minicom program like "Procomm for Linux".
Run an executable in the current directory, which is not on your PATH.

# xterm

Start a X-windows window and the default windows manager. Works like typing "win" with DOS under
Win3

# startx :

Start X-windows window on the display 1 (the default is enabled on display 0). You can have
several GUI terminals running concurrently. Switching between them using <Ctrl><Alt><F7>,
<Ctrl><Alt><F8>, etc.

# xterm

(in X terminal) Start a simple X-windows terminal. Exiting will copy it
(in X terminal) Very nice, old-fashioned game. Many games/programs are installed on
your system.... Use your mouse right button to get local menus.

# xoing

(in X terminal) A humble looking but very powerful image editor. It takes longer to use, but it is
great for artists. Use your mouse right button to get local menus.

# gimp

(in X terminal) Netscape requires a Netscape installation. The current versions of Netscape
(4.x) are known to be big and buggy. Occasionally crash by vanishing (no other harm done). Also,
when not connected to the network, Netscape likes to refuse to do anything (looks like it hanged-it
revives when you connect.

# netscape

(in X terminal) Netscape run on the current machine and direct the output to machine named "host"
(typically given by executing the command current_machine_name in the terminal of
the machine.

# netscape-display
host:0.0

(as root) Shut down the system to a halt. Mostly used for remote shutdown. Use <Ctrl><Alt><Del> for
a shutdown at the console (which can be done by any user).

# halt
reboot

(as root, two commands) Halt or reboot the machine. Use for remote system, shutdown to trigger the
previous command.

# man topic

Display the contents of the man pages (on help) first. Press "q" to
quit the viewer. The command "info topic" works and may contain many up-to-date
information. Manual pages are hard to read. Try "any_command --help" for short, easy to
gest on a command. If more need info, look to the directory /usr/doc

# apropos topic

Give me the list of commands that have something to do with my topic.

# 6.4 Process control
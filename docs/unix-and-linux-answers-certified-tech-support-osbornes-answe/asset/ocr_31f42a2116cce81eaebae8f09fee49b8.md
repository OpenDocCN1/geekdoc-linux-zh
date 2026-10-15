Voilà! Maybe someday soon your UNIX vendor will get with the program and make this workaround unnecessary, but in the meantime you have a way to get mv across filesystems.

# CONNECTING TO THE LARGER WORLD

# What is ftp and how do I go about using it?

ftp is short for file transfer protocol. If you have to transfer files between different machines running different operating systems, such as from a UNIX machine to a DOS or MS Windows PC, your best bet is probably ftp because it is supported on a broad range of platforms and operating systems. We won’t go into all the different commands that ftp supports, or all the ways that it can be used, but a typical ftp session might go something like this.

+   1. Start **ftp** by typing **ftp** on the command line. At this point, you can add the hostname of the machine you want to initially connect to. The available options are:
+      - **-d**  Enables debugging mode
+      - **-g**  Disables filename globbing
+      - **-i**  Disables interactive prompting
+      - **-n**  Doesn’t automatically log in upon initial connection
+      - **-v** **verbose**  Shows additional information about what is happening
+      - **-t**  Turns on packet tracing
+   2. Next you will connect to the remote site using **open host**, where host may be a simple local hostname, or a fully qualified hostname if you are attempting to connect to a remote machine.
+   3. You will be prompted for an account and a password on the remote system. If you are out on the Internet, and are trying to get a file that someone told you about but you don’t have an account on the remote machine, use **anonymous** as the user, and when prompted for the password, answer with your email address.
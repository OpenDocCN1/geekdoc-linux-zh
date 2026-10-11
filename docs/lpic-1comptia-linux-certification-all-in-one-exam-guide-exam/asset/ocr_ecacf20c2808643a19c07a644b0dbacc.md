# Accelerated Review

+   Linux offers both command-line and graphical user interfaces.  
+       The Linux command-line interface is created by shells.  
+       The bash shell is the default shell for most distributions.  
+       Linux shells do not search the current directory when running a file from the command prompt.  
+       Shells used to log in to the system are login shells.  
+       Shells opened after the user has logged in are non-login shells.  
+       The .bashrc file is used to configure non-login shells.  
+       The /etc/profile file is the first file read when creating a login shell.  
+       After the /etc/profile file is read, the bash shell looks for one of the following configuration files in the user’s home directory:

+   .bash_profile  
+       .bash_login  
+       .profile

+   The first of these files found is the one used to configure the user’s shell environment.  
+       The bash shell saves your command history in .bash_history.  
+       Pressing the UP ARROW key displays the last commands entered at the shell prompt.  
+       The bash shell offers command completion using the TAB key.  
+       Manual (man) pages are one of the primary means for maintaining documentation on a Linux system.  
+       Manual pages are viewed using the man utility.  
+       Manual pages are maintained for most commands, utilities, services, and configuration files on your system.  
+       The location of the man pages in your file system is stored in the MANPATH environment variable or in the MANPATH directive in the /etc/man.config file.  
+       All of the man pages together compose the manual.  
+       The manual is divided into the following sections:

+   Section 1: User programs and shell commands  
+       Section 2: Kernel functions  
+       Section 3: Library functions  
+       Section 4: Special files found in /dev  
+       Section 5: File format descriptions and conventions  
+       Section 6: Games  
+       Section 7: Miscellaneous conventions
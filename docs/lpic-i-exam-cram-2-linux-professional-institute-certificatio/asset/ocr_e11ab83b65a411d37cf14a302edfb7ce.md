+   11. Run the `configure` script with the following command:
+   `./configure`

+   12. When done, run the `make` command to compile the software.

+   13. When finished compiling, install the program with the `make install` command.

> If you get a message about not being able to install the target directory, you need to become the root user with the command `su` and enter the root user password. This is necessary in some cases so that the compiled software can be written to directories such as `/usr/local/bin` that are not write-enabled for normal users.

+   14. Rerun the `make install` command if you had to become the root user.

+   15. Make sure you're running X and have a Windows machine to connect to via Terminal Services or Remote Desktop Connection; then type the following:
+   `rdesktop -g 1024x768 IPADDRESS`

+   16. Substitute your TS or RDP machine's IP address for `IPADDRESS`. You should be able to sign on to that machine with full color and even set the client to full screen with a little reading of the help screen for rdesktop.

# Shared Libraries

Libraries provide access to common functions, with shared libraries providing common functions for many different programs on Linux systems. Programs link libraries in one of two ways:

+   * **Statically**—Has a larger file size and less dependencies

+   * **Dynamically**—Has a smaller file size and won't work if missing

A good example of shared libraries is the use of system calls to open a file, get a file's information from the inode with the stat call, and many other very common functions.

The system's main shared libraries are stored in the following:

+   * `/lib`—Main shared libraries

+   * `/usr/lib/`—Supplemental libraries

+   * `/usr/X11R6/lib`—X Window shared libraries
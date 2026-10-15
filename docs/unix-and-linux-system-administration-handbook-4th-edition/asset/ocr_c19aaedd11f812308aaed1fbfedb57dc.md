Examples of restricted operations are

+   - Changing the root directory of a process with chroot
+   - Creating device files
+   - Setting the system clock
+   - Raising resource usage limits and process priorities
+   - Setting the system’s hostname
+   - Configuring network interfaces
+   - Opening privileged network ports (those numbered below 1,024)
+   - Shutting down the system

An example of superuser powers is the ability of a process owned by root to change its UID and GID. The login program and its window system equivalents are a case in point; the process that prompts you for your password when you log in to the system initially runs as root. If the password and username that you enter are legitimate, the login program changes its UID and GID to your UID and GID and starts up your user environment. Once a root process has changed its ownerships to become a normal user process, it can’t recover its former privileged state.

# Setuid and setgid execution

Traditional UNIX access control is complemented by an identity substitution system that’s implemented by the kernel and the filesystem in collaboration. The system is described in more detail on page 153; the short version is that it allows specially prepared executable files to run with elevated permissions, usually those of root. This mechanism lets developers and administrators set up structured ways for unprivileged users to perform privileged operations.

When the kernel runs an executable file that has its “setuid” or “setgid” permission bits set, it changes the effective UID or GID of the resulting process to the UID or GID of the file containing the program image rather than the UID and GID of the user that ran the command. The user’s privileges are thus promoted for the execution of that specific command only.

For example, users must be able to change their passwords. But since passwords are stored in the protected /etc/shadow file, users need a setuid passwd command to mediate their access. The passwd command checks to see who’s running it and customizes its behavior accordingly: users can only change their own passwords, but root can change any password. (This, incidentally, is yet another example of UNIX’s ad hoc access control—the rules are written into the code of the passwd command.)

# 4.2 MODERN ACCESS CONTROL

The preceding discussion leaves out a few details, but no major concepts in the traditional UNIX model have been omitted. Even though the traditional access control system can be summarized in a couple of pages, it has stood the test of time because it’s simple, predictable, and capable of handling the majority of
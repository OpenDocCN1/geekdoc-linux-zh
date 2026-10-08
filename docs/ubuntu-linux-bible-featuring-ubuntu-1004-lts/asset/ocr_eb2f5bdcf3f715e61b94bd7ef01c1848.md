# Part II: Ubuntu for Desktop Users

# Tip

A term that you will frequently hear when discussing shells, Linux, or in general is the term shell script. A shell script is a command file containing commands that are either internal to the shell (such as those for setting variables, conditional expressions, and looping constructs) or reference other commands on your Linux system. The ability to write very sophisticated command files is a feature of the Linux/UNIX utility model, where each utility does one thing and does it well, and many different utilities can be linked via pipes or temporary files to process each other's output.

For additional information about shells on UNIX systems, see:
www.softpanorama.org/People/Shell_giants/introduction.shtml
www.faqs.org/faqs/unix-faq/shell/shell-differences/
www.unix.org.ua/orelly/unix/ksh/ch01_03.htm

# Available Shells for Linux Systems

A Ubuntu distribution installs only the standard GNU bash shell. However, other shells are available for installation through apt-get or the Synaptic Package Manager. The following shells are found on many Linux systems:

+   * /bin/ash: The Almquist shell, a small-footprint shell that began as a clone of the SYS R4 version of the Bourne shell. The shell is often used on embedded systems or during the system startup and installation process on some Linux distributions.
* /bin/bash: The default, Bourne-Again shell inspired by /bin/sh and /bin/ksh. This is the default login shell installed and used by all users on Ubuntu systems.
* /bin/csh: If you install tcsh (see its description later in this list), a symbolic link from /bin/ksh to /tcsh is also created. This link is provided to support shell scripts that reference the traditional location of the C-shell, the standard shell used on Berkeley Unix (BSD) system and its descendants. The C-shell supports configuration commands that are reminiscent of C-language programming constructs and was originally written by Bill Joy, a later founder of Sun Micros.
* /bin/dash: The Debian Almquist shell, the Debian Linux's version of the standard Almquist shell. This is used during the system boot process.
* /bin/ksh: If you install pdksh (see its description later in this list), a symbolic link from /bin/ksh to /pdksh is also created. This link is provided to support shell scripts that reference the traditional location of the Korn shell, the standard shell used on later SYSV UNIX systems from AT&T and its descendants.
* /bin/nash: Another small-footprint shell used during the startup process on many Linux systems, specifically on Red Hat and Fedora Core Linux systems
* /bin/pdksh: An open source version of David Korn's Korn shell, written at AT&T and with the SYS R3 (as part of the 'Experimental Toolchest') and R4 (as a completely supported utility) UNIX distributions. The Korn shell (and thus pdksh) is completely backward-compatible
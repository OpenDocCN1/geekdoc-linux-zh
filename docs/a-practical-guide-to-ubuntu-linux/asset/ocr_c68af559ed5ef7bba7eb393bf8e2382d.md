A filter processes another program's output, altering it as a result. The filter's output
then becomes input to another program.

Pipes and filters frequently join utilities to perform a specific task. For example, you
use a pipe to send the output of the sort utility to head (a filter that lists the
ten lines of its input); then you can use another pipe to send the output of head to a
third utility, lpr, which sends the data to a printer. Thus, in one command line, you
use three utilities together to sort and print part of a file.

# SYSTEM ADMINISTRATION

On a Linux system the system administrator is frequently the owner and only user
of the system. This person has many responsibilities. The first responsibility may
be set up the system, install the software, and possibly edit configuration files.
Once the system is up and running, the system administrator is responsible for
downloading and installing software (including upgrading the operating system),
backing up and restoring files, and managing such system facilities as printers, ter-
minals, servers, and a local network. The system administrator is also responsible
for setting up accounts for new users on a multiuser system, bringing the system
u and as needed, monitoring the system, and taking care of any problems
that arise.

# ADDITIONAL FEATURES OF LINUX

The developers of Linux included features from BSD, System V, and Sun Micros-\ystems' Solaris, as well as new features, in their operating system. Although most of
tools found on UNIX exist for Linux, in some cases these tools have been
replaced by more modern counterparts. This section describes some of the popular
tools and features available under Linux.

# GUIS: GRAPHICAL USER INTERFACES

The Window System (also called X or X11) was developed in part by researchers at
MIT (Massachusetts Institute of Technology) and provides the foundation for the
GUIs with Linux. Given a terminal or workstation screen that supports X, a
user can interact with the computer through multiple windows on the screen, display
graphical information, or use special-purpose applications to draw pictures, monitor
processes, or preview formatted output. X is an across-the-network protocol that
allows a user to open a window on a workstation or computer system that is remote
from the CPU generating the window.

Desktop manager Usually two layers run on top of X: a desktop manager and a window manager. A desk-top manager is a picture-oriented interface that enables you to interact with system
programs by manipulating icons instead of typing the corresponding commands to a shell.
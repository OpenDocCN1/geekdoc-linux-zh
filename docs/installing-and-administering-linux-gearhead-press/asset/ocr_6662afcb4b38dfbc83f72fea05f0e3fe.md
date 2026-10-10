and why you might, or might not, customize it. Topics covered include techniques to undertake any desired Linux environment customization, the use of aliases for certain commands so that you can remember or execute them more easily, and methods for manipulating and re-executing previously executed commands in a fast and easy manner.

# Variables and the Terminal Environment

Before we can discuss variables in detail and their influence on the Linux terminal and shell environments, it is worthwhile to first define variables and the terminal environment.

A *variable* is a name that is known to a program and that represents data. Although the value of the data might remain constant, it more likely changes one or more times while the program is running.

The *terminal environment* is basically the set of all variables and shell functions to which all your shells and their commands, utilities, and other processes have access. The terminal environment is thus the set of variables that all those commands, utilities, and processes have in common, but it is not some all-encompassing set of all variables from all shells. This definition varies from the more classic definition of a terminal environment; that is, the list of variables pertaining only to your computer terminal (the ones you can see by typing *stty -a* at the command line). For our purposes, the variables in the terminal environment include the *stty* variables and variables exported to the environment by various profiles, daemons, startup files, and even the shells themselves as your system was configured (as it starts up and as you log in).

As you learn more about Linux, you will no doubt customize your terminal environment by altering the values of existing variables and by defining and exporting other variables into your environment. You can rely on the variables that shipped with your distribution and that were initialized during your installation and configuration, or you can add to or change them as you become more familiar with variable and process functionality.

How do you identify the variables in your terminal environment and their respective values? Go to a command line and type *env*.

At some point, you might decide that one or more of these shell variables should be added to your environment so that you do not have to keep defining them from session to session or from shell to shell. How do you add variables to your terminal environment? If you are in the *bash* shell, you first set the shell variable by typing
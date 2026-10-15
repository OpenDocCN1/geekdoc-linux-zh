zips to the fi before resuming execution of the commands.

If you’re thinking that there are a tremendous number of ways to configure your shell, you are correct. You can have an incredibly diverse set of commands in both your .profile and .bashrc files, enabling you to customize many aspects of the shell and the Unix environment. If you use the C shell or the tcsh shell, the configuration information is kept in a similar file, called .login.

# Summary

Armed with the information learned in this hour about shells and shell environments, explore your own environment; examine your .profile and .bashrc files also.

# Workshop

The Workshop summarizes the key terms you’ve learned and poses some questions about the topics presented in this lesson. It also provides you with a preview of what you will learn in the next hour.

# Key Terms

command alias An alias is a shorthand command mapping, with which you can define new command names that are aliases of other commands or sequences of commands. This is helpful for renaming commands so that you can remember them or for having certain flags added by default.

command history The shell uses this mechanism to remember what commands you have entered already and to allow you to repeat them without having to type the entire command again.

job control Job control enables you to manage the various programs that are running. It lets you push programs into the background and pull them back into the foreground as desired.

login shell This is the shell you use, by default, when you log in to the system.

subshell This is a shell other than the login shell, which is invoked from within the login shell or another program (for example, by typing bash at the command line or by calling the shell from within emacs).

# Exercises

+   1. Draw lines to connect the original shells with their newer variants:
+      sh
+      ksh
+      tcsh
+      csh
+      bash

+   2. What does chsh do?

+   3. What shell are you running? What shells are your friends on the system running?
# # SOLVING PROBLEMS

As the system administrator, it is your responsibility to keep the system secure and running smoothly. When a user is having a problem, it usually falls to the administrator to help the user get back on track. This section suggests ways to keep users happy and the system functioning at peak performance.

# ## HELPING WHEN A USER CANNOT LOG IN

When a user has trouble logging in on the system, the source may be a user error or a problem with the system software or hardware. The following steps can help determine where the problem is:

+   * Determine whether only that one user or only that one user’s terminal/workstation has a problem or whether the problem is more widespread.
+   * Check that the user’s \texttt{CAPSLOCK} key is not on.
+   * Make sure the user’s home directory exists and corresponds to that user’s entry in the \texttt{/etc/passwd} file. Verify that the user owns his or her home directory and startup files and that they are readable (and, in the case of the home directory, executable). Confirm that the entry for the user’s login shell in the \texttt{/etc/passwd} file is valid (that is, the entry is accurate and the shell exists as specified).
+   * Change the user’s password if there is a chance that he or she has forgotten the correct password.
+   * Check the user’s startup files (\texttt{.profile}, \texttt{.login}, \texttt{.bashrc}, and so on). The user may have edited one of these files and introduced a syntax error that prevents login.
+   * Check the terminal or monitor data cable from where it plugs into the terminal to where it plugs into the computer (or as far as you can follow it). Try turning the terminal or monitor off and then turning it back on.
+   * When the problem appears to be widespread, check whether you can log in from the system console. If you can, make sure that the system is in multiuser mode. If you cannot log in, the system may have crashed; reboot it and perform any necessary recovery steps (the system usually does quite a bit automatically).
+   * Check that the \texttt{/etc/event/tty\[1-6\]} files to see if \texttt{mingetty} is starting with certain events (\texttt{FEDORA}). Check that the \texttt{/etc/inittab} file is set up to start \texttt{mingetty} at runlevels 2--5 (\texttt{SUNOS}).
+   * Check the \texttt{/var/log/messages} file. This file accumulates system errors, messages from daemon processes, and other important information. It may indicate the cause of more symptoms of a problem. Also, check the
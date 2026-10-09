+   e. Type ps
+   f. Press <Enter>

Your screen will look like Figure 3-14. Note that the shell listed is now csh.

PID     TTY      TIME     COMMAND
829     tty4     00:00:04 login
835     tty4     00:00:04 csh
892     tty4     00:00:00 ps

Figure 3-14 Output of ps Shows the New Login Shell

+   15. The *Linux Made Easy* CBT uses bash. In this exercise, you will change back to bash.

+   a. At the shell prompt, type csh.
+   b. Press <Enter>
+   c. Type in your password.
+   d. Press <Enter>
+   e. Type /bin/bash. This will call up bash.
+   f. Press <Enter>
+   g. Press <Ctrl-D> to log out.
+   h. Use the standard login procedure, by entering your *userid* and password.

Note that to complete the process of changing back to bash, you had to log out and then log back in.

+   16. If your Linux installation permits, log in at a second terminal. Now repeat Exercise 10.

+   a. Type ps -a
+   b. Press <Enter>

Note that this time you are using a lowercase “a.”

You will see two copies of your shell listed—one for each terminal you log in from. This reminds you that, each time you log in, you start a new copy of your shell and each copy is a separate process. Compare the “tty” column listing with each shell process; you will see two different terminal numbers.
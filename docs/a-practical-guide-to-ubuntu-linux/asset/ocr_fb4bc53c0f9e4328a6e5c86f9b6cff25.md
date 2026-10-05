# SOLVING PROBLEMS 617

+   * Check the log files in /var/log. The /var/log/messages file accumulates system errors, messages from daemon processes, and other important information. It may indicate the cause or symptoms of a problem. Also, check the system console. Occasionally messages system problems that are not written to /var/log/messages (for instance, a full disk) are displayed on the system console.

+   * Determine whether only that user or only that one user's terminal/workstation has a problem or whether the problem is more widespread.

+   * Check that the user's CAPS LOCK key is not on.

+   * Make the user's home directory exists and corresponds to that user's entry in the /etc/passwd file. Verify that home and startup files are readable (and, in the case of the user's home directory, executable). Confirm that the entry for the user's login shell in /etc/passwd file is accurate and the shell exists as specified.

+   * Change the user's password if there is a chance he has forgotten the correct password.

+   * Check the user's startup files (.profile, .login, .bashrc, and so). The user may have edited one of these files and introduced a syntax error that prevents login.

+   * Check the terminal or monitor data cable from where it plugs into the computer (or as far as you can follow it). Try turning the terminal or monitor off and then turning back on.

+   * When the problem appears to be widespread, check whether you can log in from the system console. Make sure the system is not in recovery mode. If you cannot log in, the system may have crashed; reboot it and perform any necessary recovery steps (the system usually does quite a bit automatically).

+   * If the user is logging in a network connection, run the appropriate script (page 440) to restart the service the user is trying to use (e.g., ssh).

+   * Use df to check for all filesystems. If the /tmp filesystem or the user's home directory is full, login sometimes fails in unexpected ways. You may be able to log in to a textual environment but not a graphical one. When applications start the user log in can create temporary files or cannot update files in the user's home directory, the login process itself may terminate.

# SPEEDING UP THE SYSTEM

When the system is running slowly for no apparent reason, perhaps a process did exit when a user logged out. Symptoms of this problem include poor response time and system load, as shown by w or uptime, that is greater than 1.0. Running top (page 610) is an excellent way to find rogue processes quickly. Use ps -ef to list all processes. One thing to look for in ps -ef output is a large number in the TIME
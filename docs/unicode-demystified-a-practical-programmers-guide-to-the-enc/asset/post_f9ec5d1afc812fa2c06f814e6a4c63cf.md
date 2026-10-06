
# Helping When a User Cannot Log In

When a user has trouble logging in on the system, the problem may be a user error or a problem with the system software or hardware. These steps help you determine where the problem is.

- 1. Determine whether only that one user or only that user's terminal/workstation has a problem or whether the problem is more widespread.
- 2. If a single user has a problem, perhaps the user does not know how to log in. The user's terminal will respond when you press RETURN, and you will be able to log in as yourself. Make sure that the user has a valid login name and password; then show the user how to log in.
- 3. Make sure that the user's home directory exists and corresponds to that user's entry in the /etc/passwd file. Verify that the user owns his or her home directory and startup files and that they are readable (and, in the case of the home directory, executable). Confirm that the entry for the user's login shell in /etc/passwd file is valid (that is, the entry is accurate and that the shell exists exactly as specified).
- 4. Change the user's password if there is a change that he or she has forgotten the correct password.
- 5. Check the user's startup files (.profile, .login, .bashrc, and so on). The user may have edited one of these files and introduced a syntax error that prevents login.
- 6. If only that one user's terminal has a problem, other users will be using the system, but that user's terminal will not respond when you press RETURN. For a serial terminal, try pressing the BREAK and RETURN keys alternately to reestablish the proper connection rate, and make sure that the terminal is set for a legal connection rate, such as 9600 bps. For any terminal/workstation try pressing the keys listed in Table 17-23.

| Key | Table 17-23 |
|---|---|
| CONTROL-Q | Unsticks the terminal if someone pressed CONTROL-S. |
| interrupt | Stops a runaway process that has hung the terminal. The interrupt key is usually CONTROL-C. |
| ESC | Helps if the user is in input mode in vi. |
| CONTROL-L | Redraws the screen if the user was using vi. |
| CONTROL-MRESETCONTROL-M | Resets a character-based terminal. |
| CONTROL-R | An alternative for CONTROL-L. |
| CONTROL-X CONTROL-C | Gets the user out of emacs. |
| ESCq RETURN | Gets the user out of ex or vi. |

- 7. Check the terminal or monitor data cable from where it plugs into the terminal to where it plugs into the computer (or as far as you can follow it). Finally trying the terminal or monitor off and then turning it back again.
- 8. When the problem appears to be widespread, check whether you can log in from the system console. If you can, make sure that the system has crashed; reboot it and perform any necessary recovery steps (the system usually does quite a bit automatically).
- 9. Check the /etc/initab file to see that it is starting the appropriate login service (usually some from getty, such as mingetty).
- 10. Check the /var/log/messages file. This accumulates system errors, the messages from daemon processes, and other important information. It may indicate the cause or more symptoms of a problem. Also, check the console of the machine. Occasionally messages about system problems that do not get written to /var/log/messages (for instance, if the disk is full) get displayed on the console.
- 11. If the user is logging in over a network connection, use "redhat-configs: Configure Services II" on page 946, "chkconfig: Configure Services III" on page 947, or "ntsysv: Configure Services IV" on page 948 to make sure that the service the user is trying to use (such as telnet or ssh) is enabled.
- 12. Use df to check for full filesystems. Sometimes if the /tmp filesystem or the user's home directory is full, the login fails in unexpected ways. When applications that start when the user logs in cannot create temporary files or cannot update files in the user's home directory, the login process itself may terminate.

# Speeding Up the System

When the system is running slowly for no apparent reason, perhaps a process does not exit when a user logged out. Symptoms include poor response time and a system load, as shown by w or uptime, that is greater than 1.0. Use ps -ef to list all processes. The top utility (page 1356) is excellent for quickly finding rogue processes. One thing to look in ps -ef output is a large number in the TIME field. For example, if you find a process that has a TIME field over 100.0, this process likely ran away. However, if the user is using a lot of Java work and has not logged out for a long period of time, this may be normal. Look at the STIME field to see when the process was started. If the process was running for longer than the user has logged in, it is a good candidate to kill.

When a user gets stuck and leaves his her terminal unattended without modifying anything, it is convenient to kill all processes by that user. If the user is running a window system, as GNOME or KDE on the console, kill the window manager process. Manager processes to look for include stage, gnome-session, or another process name that ends in w. Usually the window manager is either the first or last to run, and exiting from the window manager logs the user out. If killing the window manager does not work, try killing the X server process itself. This is if that fails, you can kill all processes owned by a user by running kill -1 -1, or equivalently kill -HUP -1 as the user. Using -1 (one) in place of the process ID tells kill that it should send the signal to all processes that are owned by that user. For example, as root you could type

```bash
# jenny -c 'kill -TERM -1'
```

If this does not kill processes (sometimes TERM does not kill a process), you can use the KILL signal. The following line will definitely kill processes owned by Jenny and will not be friendly about it:

```bash
# jenny -c 'KILL -1'
```

(If you do not use jenny -c, the same command brings the system down.)

# lsof: Finds Open Files

The name lsof is short for open files; this utility locates open files. Its options let you look only at certain processes, look only at file descriptors of a process, or show certain network connections (network use file descriptors just as normal files do and lsof can show those as well). Once you have identified a suspected process using ps -ef, run the following command:

```bash
# lsof -sp pid
```

Replace pid with the process ID of the suspect process; it displays a list of all file descriptors that process has open. The -s option displays the size of all open files. The size information may be helpful in determining whether the process has a very large file open. If so, contact the owner of the process, or if necessary, call the process. The -n option redisplays the output of it every n seconds.

# Keeping a Machine Log

A machine log that includes the information shown in Table 17-24 can help you find and system problems. Note the time and date for each entry in the log. Avoid the temptation to keep the log only on the computer because it will be most useful to you at times when the machine is down. Another good idea is to keep a record of all e-mail about user problems. One way to do this is to save all this to a separate file or folder. Another way is to set up a special alias that users send when they have problems. This alias can then forward mail to you and also store a copy in an archive file. Following is an example of an entry in the /etc/aliases file that sets this type of alias:

```text
trouble: admin,/var/mail/admin.archive
```

E-mail sent to the trouble alias will be forwarded to the admin user and also stored in the file /var/mail/admin.archive. Remember to run the newaliases after editing /etc/aliases.

| Condition | Table 17-24 |
|---|---|
| Hardware modifications | Keep track of the system hardware configuration: which interrupt is used for which device, what I/O addresses are needed by which card, which devices hold which partitions, and so on. |
| System software modifications | Keep track of the options used by Linux. Print such files as /usr/include/linux/autoconf.h (Linux kernel configuration), /etc/modules.conf, and /etc/X11/X86Config (X11 configuration). The file hierarchy under /etc/sysconfig contains valuable information about network configuration and so on. |
| Hardware malfunctions | Keep as accurate a list as possible of any problems with the system. Make note of any error messages or numbers that the system displays on the system console and what users were doing when the problem occurred. |
| User complaints | Make a list of all reasonable complaints made by knowledgeable users (for example, "machine is abnormally slow"). |

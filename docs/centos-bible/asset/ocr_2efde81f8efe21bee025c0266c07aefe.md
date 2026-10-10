This shows that the username is timothy, which is represented by the numeric user ID (uid) 500. Here, the primary group for timothy is also called timothy, which has a group ID (gid) of 500. timothy also belongs to other groups called wheel (gid 10) and users (gid 100). These names and numbers represent the permissions that timothy has to access computer resources.

If your computer has SELinux enabled, the id command also shows context information. In this example, you see context= unconfined_u:unconfined_r:unconfined_t on id output. SELinux is discussed later, in Chapter 9.

You can see information about your current login session by using the who command. In the following example, the -m option tells the who command to print information about the current user; -u says to add information about idle time and the process ID, and -H asks that a header be printed:

```
$ who -u -m -H
NAME      LINE         TIME          IDLE    PID COMMENT
timothy   pts/1        2009-04-02 14:12        7264 (:0.0)
```

You can put multiple single-letter options together after a single dash:

```
$ who -umH
```

The output from this who command shows that the username is timothy, the user is logged in on pts/1, and his login session began at 14:12 on April 2. The IDLE time shows how long the shell has been open without any command being typed (the dot indicates that it is currently active). COMMENT would show the name of the remote computer the user had logged in from, if that user had logged in from another computer on the network, or the name of the local X display if you were using a terminal window (such as :0.0).

> **NOTE** pts stands for pseudo terminal slave. The concept of a terminal comes from the old days, when people worked exclusively from character terminals. Today, a terminal typically represents a single person at a single screen.

# ## Checking Directories and Permissions

Associated with each shell is a location in the Linux file system known as the *current* or *working directory*. As previously mentioned, each user has a directory that is identified as the user's home directory. When you first log in to Linux, you begin with your home directory as the current directory.

When you request to open or save a file, you use the current directory as the point of reference. Simply *give a filename* when you save a file, and it will be placed in the current directory. Alternatively, you can identify a file by its relation to the current directory (known as a *relative path*). Or you can ignore the current directory and identify a file by the full directory hierarchy that locates it (known as an *absolute path*).
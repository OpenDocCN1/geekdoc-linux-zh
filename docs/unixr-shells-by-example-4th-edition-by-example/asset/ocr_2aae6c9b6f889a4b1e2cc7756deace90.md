systems are still using version 1.14.7. All versions are freely available under the GNU public license.² There is even bash for Windows! To see what version you are using, use the --version option to bash or print the value of the BASH_VERSION environment variable.

# EXAMPLE 13.1

```
(UNIX)
$ bash --version
GNU bash, version 2.05.0(1)-release (sparc-sun-solaris)
Copyright 2000 Free Software Foundation, Inc.

$ echo $BASH_VERSION
2.05.0(1)-release
```

# EXAMPLE 13.2

```
(Linux)
$ bash --version
GNU bash, version 2.05.0(1)-release (i386-redhat-linux-gnu)
Copyright 2000 Free Software Foundation, Inc.
```

# 13.1.2 Startup

If the bash shell is your login shell, it follows a chain of processes before you see a shell prompt. See Figure 13.1.
When the system boots, the first process to run is called init, PID #1. It spawns a getty process. This process opens up the terminal ports, providing a place where standard input comes from and a place where standard output and errors go, and puts a login prompt on your screen. The /bin/login program is then executed. The login program prompts for a password, encrypts and verifies the password, sets up an initial environment, and starts up the login shell, /bin/bash, the last entry in the passwd file. The bash process looks for the system directory file, /etc/profile, and executes its commands. It then looks in the user's home directory for an initialization file called .bash_profile. After executing commands from .bash_profile,³ it will execute a command from the user's .EW file, usually called .bashrc, and finally the default dollar sign ($) prompt appears on your screen and the shell waits for commands. (For more on initialization files, see "The Environment" on page 756.)

2. To get the latest version of bash, visit www.delorie.com/gnu/.

3. There are a number of different initialization files used by bash; they are discussed on the next pages.
# The Linux Cookbook: Tips and Techniques for Everyday Use:

```
# apt-get install sview RET
```

This command will upgrade the `sview` package to the most current version available, if greater than the version already installed on your system. If additional packages must be upgraded first in order for this new package upgrade to function properly, this command will fetch and upgrade those packages, too. Before downloading any packages, apt-get will show the list of packages that will be installed, replaced, or otherwise changed, and wait for confirmation first.

To bring your entire Debian system up to date, use the apt-get tool with the following command arguments. First, use the `update` argument to update your system's list of available software packages. Then run apt-get again, using either the `upgrade` argument to upgrade all of the installed packages to their most recently available versions, or use the `dist-upgrade` argument when a new version of the Debian system is announced, to upgrade to that new version.

+   - To upgrade all of the software on your system to their most recent versions, type:

```
# apt-get update RET
...processing messages...
# apt-get upgrade RET
...processing messages...
#
```

+   - To upgrade your Debian system to the most recent release, type:

```
# apt-get update RET
...processing messages...
# apt-get dist-upgrade RET
...processing messages...
#
```

# A.3.4 Installing a Shell Script

A shell script is a file that contains commands written in a shell command language (see section The Shell). You run (or "execute") a script as you would any other command (see section Running a Command). First, make sure that the script file is executable; if it isn't, you won't be able to execute it (see section Making a File Executable).

Generally, the administrator installs new shell scripts in the `/usr/local/bin` directory. If you are on a multi-user system and you are the only user liable to run a particular script, you can put it in a special directory in your home directory tree—the `~/bin` directory is the standard recommendation here—and then add that directory to your path (see section Adding to Your Path).

Not all executable script files are shell scripts. The first line of a script contains the full path name of the shell or other program that is to interpret and execute the script; sometimes, the path may differ on your system
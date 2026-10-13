> If you add a variable to /etc/rc.conf, make sure that another version of that variable isn't already in the file—or at least that it doesn't appear later on in the file. The variables are read sequentially, and the way the overrides work is simply that the last occurrence of each variable seen by the system is the one it uses. If you are always careful to add variables only to the end of rc.conf, you should be fine.

Many programs, when you install them, will have to install a way for themselves to start up at boot time; /etc/rc.conf is not, however, the place for them. That file is supposed to be touched only by you, the administrator, and by the sysinstall program when it makes changes to the core system. For user-installed programs (ports and packages) and for any scripts that /etc/rc and friends do not know about, another structure is in place for their startup scripts and configuration files: the /usr/local/etc hierarchy.

# The /usr/local/etc and /usr/local/X11R6/etc Directories

Programs that you install yourself are considered to be local, meaning that they apply only to your particular machine and not to FreeBSD itself. Configuration files for your locally installed programs go into the /usr/local hierarchy in FreeBSD as one of its structural conventions. There is a /usr/local/etc/rc.d directory, which is equivalent in operation to /etc/rc.d—except that because the files in it apply to the programs that you have installed, rather than to the core system, you can edit these files yourself in order to change those programs' behavior.

init turns its attention to /usr/local/etc/rc.d after it has run through all the other /etc/rc.d scripts. Any executable file within the directory that ends in .sh will be executed in lexicographical order. Examples of files that will be installed in here include apache.sh, mysql-server.sh, and samba.sh. These scripts are custom built as part of the ports or packages (see Hour 6, "Adding and Removing Third-Party Software," for more about the ports and packages), and each one is tuned to take a start or stop argument. When init runs each script, it uses the start argument. Note that you can run these scripts yourself during runtime just as easily—for instance, to start a newly installed service without rebooting,

```
# /usr/local/etc/rc.d/apache.sh start
```

Some ports or packages will install with a secondary suffix of .sample (for example, samba.sh.sample) because the program that it's part of has to be properly configured before it can run successfully. Apache, for instance, will run immediately after
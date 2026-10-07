The remote end of the connection (in this case, the system arthur) must have corresponding entries for `merlin`. The files will be similar with only name, telephone number, and (possibly) device name and chat script changes. Until both ends are configured properly, you can’t get a connection between the two machines.

Some Linux systems with Taylor UUCP have a utility called `uuchck` that verifies the syntax in the UUCP configuration files and printout summary information. If you don’t have the `uuchck` utility, it can be downloaded from many FTP and BBS sites. Check Appendix A, “Linux FTP Sites and Newsgroups,” for some of the possible sites.

By default, Taylor UUCP allows a remote system to execute only a limited number of commands when they log into your system. Typically, the remote is only allowed to execute `rmail` and `rnews`, to transfer mail and news respectively. If you want to allow extra programs to be executed, add a line to the `/usr/lib/uucp/sys` file that includes all the commands the remote system can execute. For example, the following entry specifies that the system chatten can execute any of the four commands given after the commands keyword:

```
system       chatten
...
commands       rmail rnews rsmtp rdataupdate
```

Note that all four commands must be in the usual search path used by the UUCP utilities (actually by `uuxqt`).

If you intend to transfer files between two machines, you must also modify the configuration files. When a remote system sends a file to your machine, the files should usually be stored in the directory `/usr/spool/uucppublic` (some systems use `/var/spool/uucppublic`) as a safety precaution. You don’t want to allow a remote system to write files anywhere on your file system or they could overwrite critical system files. The convention for most UUCP systems is to use either `/usr/spool/uucppublic` or `/usr/spool/uucp/system` (in which *system* is the remote system’s name) as the transfer directories.

You can specify transfer and receive directories in the `/usr/lib/uucp/sys` file. For example, the following entry for the remote system chatten has been modified to include specific directories for file transfers:

```
system       chatten
...
local-send      ~/send
local-receive   ~/receive
```

In this configuration, the users on your local machine can send any file that is in the send directory under the uucp directory (`~/send`, which means that any file to be sent to a
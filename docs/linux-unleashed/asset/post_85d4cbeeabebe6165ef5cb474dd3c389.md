
available for the latter. If you have one of these scripts, by all means use it, but do check the files manually afterward.

For the configuration processes discussed in the following section, we will assume that our host machine's name is merlin, and we want to connect via UUCP to another Linux system called arthur. As you go through the process, take care to enter the information in the same format as the examples, but don't mix Taylor and HDB UUCP information.

## Taylor UUCP Configuration

We can begin with a quick look at the configuration files involved in the Taylor UUCP system. These are the filenames and their primary purposes:

- `/usr/lib/uucp/config`—Defines the local machine name.
- `/usr/lib/uucp/sys`—Defines the remote systems and how to call them.
- `/usr/lib/uucp/port`—Describes each port for calling out and its parameters.
- `/usr/lib/uucp/dial`—Describes the dialers for calling out.
- `/usr/lib/uucp/dialcodes`—Used to contain expansions for symbolic dialcodes but is rarely used when a straight-out telephone connection exists.
- `/usr/lib/uucp/call`—Can contain the login name and password for remote systems, but it is rarely used now.
- `/usr/lib/uucp/passwd`—Contains the login names and passwords used when remote systems connect to your local machine. Used only when `uucico` is password checking instead of using the login process.

To make the configuration process easier, we will ignore all the theory and background information and proceed with a sample configuration. You need only modify the entries to suit your own names, telephone numbers, device files, and so on, and the configuration process will be the same. It can then be repeated for as many systems as you want to connect to.

The first file to modify holds your system name and other general parameters. The file `/usr/lib/uucp/config` needs a single line entry for your system name such as this one:

```
nodename merlin
```

The keyword `nodename` must be first on the line followed by whitespace (spaces or tabs), then your machine name. The information in this file may have been completed when you installed Linux, but you should manually check the contents to make sure. If your system's name isn't set correctly, the connection to the remote system won't work properly.

![](img/e8e6b47ac20475e23d48b4c476f5d891_720_0.png)

> **TIP**
> To use UUCP, you must have a system name. For compatibility with most versions of UUCP, keep the name to seven characters or fewer. Ideally, the UUCP name is the same name you assigned to your host during configuration. The name doesn't have to follow a convention (such as the system name used by TCP/IP for Internet access), but if you use other network protocols, keep a consistent name. If you have a domain name (for TCP/IP access) use the first component of the machine's full TCP/IP name as the UUCP name. For example, if your full domain name is `merlin.wizards.com`, use the UUCP name `merlin`.

You also need information about the remote system you want to connect to. The `/usr/lib/uucp/sys` file holds all the information about remote systems. This file usually has a few sample entries in it, which you can copy or modify. Make sure you don't leave comment marks (pound or hash marks) in the first column or the entries will be ignored. A `/usr/lib/uucp/sys` entry for the remote machine `merlin` looks like this:

```
# system: arthur (Bill Smallwood's Linux system)
system  arthur
time  Any
phone  555-1212
port  com1
speed  9600
chat  login: merlin password: secret1
```

The first line in the preceding extract is a comment line. Most system administrators like to put a comment line in to identify each system. The next lines identify the different aspects of the remote system, including its name (`arthur`), times at which it can be called (`Any` in this case, meaning no restrictions), the telephone number (including any area code or special digits that have to be dialed), the serial port to be used for the connection (in this case, `com1`), the speed at which to connect (9600 baud), and the chat script or login process. In this case, the chat script tells UUCP to wait until it sees the string `login:`; then to send `merlin`, wait for the prompt `password:`, and then send `secret1`.

Most login scripts require a login and password, and they must be placed in the configuration file because UUCP doesn't allow interactive sessions. This can be a bit of a problem because it allows other users on your system to see the login password for the remote machine, but because it can only be used by UUCP, this is not a major concern. Also, the file permissions on the UUCP configuration files can be set to prevent any system users (other than `root`) from looking into the file.

> **TIP**
> Not all remote sites need a password for entry through UUCP. For example, some public archives let you log in and retrieve files using the `uucp` login with no password. Some sites use readily available passwords, such as `uucp`.

The port name used in the `/usr/lib/uucp/sys` entry does not have to match a device name on the Linux system because another file is used to match the entry to a physical device. This file is `/usr/lib/uucp/port`, and it requires an entry similar to this for a 9600 baud modem:

```
# com1 device port
port       com1
type       modem
device     /dev/cua0
speed      9600
dialer     Hayes
```

In the `/usr/lib/uucp/port` file, the name of the port used in the `/usr/lib/uucp/sys` file is identified on the first line. The type of connection to be used (usually modem) is on the next. The actual Linux device that corresponds to the port name is specified as a device driver (for many Linux systems this can be `/dev/modem` which is linked to the serial port device driver).

The modem connection speed comes next and shows the maximum speed at which the modem can be used. Finally, the name of a dialer is entered. This is a throwback to the days when modems couldn’t dial themselves but used another device (called a `dialer`) to make the connection.

The dialer entry in the `/usr/lib/uucp/port` file is then matched to an entry in the file `/usr/lib/uucp/dial` which tells the modem how to dial the phone. Here’s a simple entry:

```
# Hayes modem
dialer      Hayes
chat        "" ATZ OK ATDT\T CONNECT
```

This shows the script that the system uses to communicate to the Hayes modem. In this case, the `\T` in the command line is replaced with the telephone number to be called. Some Linux systems simplify the use of the `/usr/lib/uucp/port` and `/usr/lib/uucp/dial` files into one single entry in the `/usr/lib/uucp/sys` file, which names the modem file directly.

The remote end of the connection (in this case, the system `arthur`) must have corresponding entries for `merlin`. The files will be similar with only name, telephone number, and (possibly) device name and chat script changes. Until both ends are configured properly, you can’t get a connection between the two machines.

Some Linux systems with Taylor UUCP have a utility called `uuchck` that verifies the syntax in the UUCP configuration files and printout summary information. If you don’t have the `uuchck` utility, it can be downloaded from many FTP and BBS sites. Check Appendix A, “Linux FTP Sites and Newsgroups,” for some of the possible sites.

By default, Taylor UUCP allows a remote system to execute only a limited number of commands when they log into your system. Typically, the remote is only allowed to execute `rmail` and `rnews`, to transfer mail and news respectively. If you want to allow extra programs to be executed, add a line to the `/usr/lib/uucp/sys` file that includes all the commands the remote system can execute. For example, the following entry specifies that the system `chatten` can execute any of the four commands given after the `commands` keyword:

```
system       chatten
...
commands       rmail rnews rsmtp rdataupdate
```

Note that all four commands must be in the usual search path used by the UUCP utilities (actually by `uuxqt`).

If you intend to transfer files between two machines, you must also modify the configuration files. When a remote system sends a file to your machine, the files should usually be stored in the directory `/usr/spool/uucppublic` (some systems use `/var/spool/uucppublic`) as a safety precaution. You don’t want to allow a remote system to write files anywhere on your file system or they could overwrite critical system files. The convention for most UUCP systems is to use either `/usr/spool/uucppublic` or `/usr/spool/uucp/system` (in which `system` is the remote system’s name) as the transfer directories.

You can specify transfer and receive directories in the `/usr/lib/uucp/sys` file. For example, the following entry for the remote system `chatten` has been modified to include specific directories for file transfers:

```
system       chatten
...
local-send      ~/send
local-receive   ~/receive
```

In this configuration, the users on your local machine can send any file that is in the `send` directory under the `uucp` directory (`~/send`, which means that any file to be sent to a

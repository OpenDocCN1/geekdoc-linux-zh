who prefer the tried-and-true command-line approach to system administration. However, most system administrators will admit that GUI-based tools reduce the number of configuration errors in complex tables. They also assist new systems administrators in tailoring unfamiliar applications.

There is an ever-growing collection of GUI administration tools directed at simplifying Samba configuration and in this chapter we'll take a brief tour of some of them. Before we delve into the color-filled, form-based world of GUI tools, let's start with good old command-line tools.

# Command-Line Tools

# testparm

An excellent command-line tool for verifying general smb.conf correctness is the Samba testparm command. testparm will not guarantee that a particular share or section will operate the way you expect, rather it will validate the syntax and parameters you have specified for each section in the configuration file. Invoke testparm with the full path name of the target smb.conf file as an argument. If a host name or IP address is supplied as an option, it will also check the access rights of the specified host. See the testparm (1) man page for additional information.

```
$ testparm <-s configfilename> <hostname hostIP>
```

# smbclient

We talked about using the smbclient command a number of times in the text to validate access to servers and services. smbclient can be used to move files between file shares, modify files and directories, print files on remote printers and exercise NetBIOS name-to-address resolution. Refer to Chapter 13 "Samba Clients" and the smbclient (1) man page for detailed information on smbclient options.

```
$ smbclient -L <server> -N
```

# smbstatus

The smbstatus command is a simple tool that will display information about active connections to your server. Server status information can be limited to users, shares or locks. This is a useful tool for making a quick check on the general health of the server. See the smbstatus (1) man page for options and additional information.

```
$ smbstatus -d
```

# testprns

Verify that the printer name is a valid entry in the printer configuration file with the testprns command. See the testprns (1) man page for more information.

```
$ testprns <printer name> <printcap file>
```

# Web Tools
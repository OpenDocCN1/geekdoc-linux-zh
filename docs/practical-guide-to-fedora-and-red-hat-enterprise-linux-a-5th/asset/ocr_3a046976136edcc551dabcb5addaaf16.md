# **scp: COPIES FILES FROM/TO A REMOTE SYSTEM**

The *scp* (secure copy) utility copies an ordinary or directory file from one system to another on a network. This utility uses *ssh* to transfer files and employs the same authentication mechanism as *ssh*; thus it provides the same security as *ssh*. The *scp* utility asks you for a password when one is required. The format of an *scp* command is

```
scp [user@][from-host:]source-file [user@]to-host:]destination-file]
```

where *from-host* is the name of the system you are copying files from and *to-host* is the system you are copying to. The *from-host* and *to-host* arguments can be local system names, FQDNs (page 1083) of systems on the Internet, or IP addresses. When you do not specify a host, *scp* assumes the local system. The *user* on either system defaults to the user on the local system who is giving the command; you can specify a different user with *user*@. The *scp* utility can copy between two remote systems.

The *source-file* is the file you are copying, and the *destination-file* is the resulting copy. Make sure that you have read permission for the file you are copying and write permission for the directory you are copying it into. You can specify plain or directory files as relative or absolute pathnames. (A relative pathname is relative to the specified or implicit user’s home directory.) When the *source-file* is a directory, you must use the *-r* option to copy its contents. When the *destination-file* is a directory, each of the source files maintains its simple filename. When the *destination-file* is missing, *scp* assumes the user’s home directory.

Sam has an alternate username, *sls*, on *grape*. In the following example, Sam uses *scp* to copy *memo.txt* from the home directory of his *sls* account on *grape* to the *allmemos* directory in the working directory on the local system. If *allmemos* was not the name of a directory, *memo.txt* would be copied to a file named *allmemos* in the working directory.

```
$ scp sls@grape:memo.txt allmemos
sls@grape's password:
memo.txt        100%  |************************************|  14664      00:00
```

As the transfer progresses, the percent and number of bytes transferred increase and the time remaining decreases. The asterisks provide a visual representation of the progress of the transfer.

In the next example, Sam, while working from *peach*, copies the same file as in the previous example to the directory named *old* in Sam’s home directory on *speedy*. For this example to work, Sam must be able to use *ssh* to log in on *speedy* from *grape* without using a password. For more information refer to “Authorized Keys: Automatic Login” on page 634.

```
$ [sam@peach]  scp sls@grape:memo.txt speedy:old
sam@grape's password:
```
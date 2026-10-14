
Four different types of ratios exist: UserRatio (used to set ratios on a user or all users), HostRatio (used to set ratios for specific hosts), GroupRatio (used to set ratios for groups), and AnonRatio (used to set a ratio for anonymous users). Each of these ratios takes five parameters in the following form:

```
RatioType String FileRatio FileCredit ByteRatio ByteCredit
```

String can be a user or for UserRatio, a hostname (including wildcards) for hosts, a group name for GroupRatio, or an email address to be matched for AnonRatio.

The remaining four parameters are all integers. FileRatio is the number of files the user has to upload in order to download a file. The FileCredit is the initial number of file credits the user gets upon connection. The ByteRatio is the ratio of upload/download in bytes. And, finally, the ByteCredit is the initial number of bytes the user gets as credit.

To understand ratios, look at the following example:

```
Ratios
on
UserRatio art 1 1 1
```

This tells proftpd to turn on Ratios and set the following rule. A user can download one file for every file he uploads, and he gets an initial credit of one file when he logs in. Therefore, when someone logs in with the username art, he can download one file without having to upload one, but any further downloading requires him to upload files in a 1:1 ratio.

The byte limit follows the same rule as the file ratio. The user gets one byte for every byte he uploads. Having a byte ratio is useful as a secondary controlling mechanism.

Let's look at another example:

```
HostRatio *.xyz.com 5 1 0
```

This rule says "For anyone connecting from xyz.com domain, set a file ratio of five to one (5:1) with an initial file credit of one file, and don't enter any byte ratio for them." Entering zero as a value will disable checking it.

To tell proftpd to enter a byte ratio of three to one (3:1) with 50,000 bytes initial credit and no file ratio for all users belonging to group staff, use the following command:

```
GroupRatio staff 0 0 3 50000
```

Thanks to ratios, you are now able to control all the file transfers that occur on your FTP server. If a user attempts to break any of these rules, the server will not allow it.

## Using the <Limit> Tag

The <Limit> tag is one of the most important tags in proftpd. It enables you to set limits on directories. This can be helpful in controlling how users interact with the directories being configured.

The <Limit> tag can be used to control the following operations:

- The ability to change the current working directory (CWD)
- The ability to make new directories (MKD)
- The ability to rename files (RNFR)
- The ability to delete files (DELE)
- The ability to remove a directory (RMD)
- The ability to retrieve a file from the server (RETR)
- The ability to transfer a file to the server (STOR)
- The ability to execute any of the reading command groups, such as RETR and STAT (READ)
- The ability to execute any of the writing command groups, such as MKD and RMD (WRITE)
- The ability to execute any of the directory listing command groups, such as LIST (DIRS)
- The ability to execute any ftp command (ALL)

As you can see from the previous list, you can set limits on individual commands or on a group of them all at once. The <Limit> is frequently used within a <Directory> context, but can be used in other contexts.

To fully understand how this tag works, let's look at an example. Suppose that you do not want your users to be able to see any part of the system other than their homes using FTP. You should first deny them the ability to see any directory in the whole system:

```
<Directory />
  <Limit DIRS>
    DenyAll
  </Limit>
</Directory>
```

Then, you should allow them to see their own homes:

```
<Directory ~>
  <Limit DIRS>
    AllowAll
  </Limit>
</Directory>
```

Now your users will be able to list only the contents of their own homes. If they try to change the current working directory to anything other than their homes, they will get a permission denied message.

This setup does have one flaw, though. If a user wants to transfer a file from another directory other than her home, she can do so if she knows the exact path to it. For instance, if a user knows that there is a file called passwords.txt in /usr/local/data, she will be able to download it by explicitly using the full path to the file. To fix this flaw, you should add READ WRITE to the first limit:

```
<Directory />
<Limit DIRS READ WRITE>
    DenyAll
</Limit>
</Directory>
```

And add it to the second one:

```
<Directory ~>
<Limit DIRS READ WRITE>
    AllowAll
</Limit>
</Directory>
```

There, now it's more secure.

You should be careful of how you order your rules. If you were to switch the positions of the previous <Directory> blocks, the effect would be that your users couldn't see, read, or write anything in their homes. The idea is to block global access and then allow certain paths.

> TIP
> Denying your users the ability to browse beyond their homes using the method we just explained can be accomplished using one tag. Using the DefaultRoot tag, you can jail your users within the boundaries of their home directories. For example, entering DefaultRoot ~ users in your configuration file will cause the root directory of any user in the group users to become that user's home directory. When that user logs in, he will not be able to move outside his home directory. It should be noted, however, that this method is not 100% secure—there are ways for a user to escape from this jail. This is why the method we explained previously is more secure.

So far, you have used the AllowAll and DenyAll tags to tell <Limit> what to do. You also can use AllowUser, AllowGroup, DenyUser, and DenyGroup to be more flexible. Each of these tags takes a user, a group, or a list of them as parameters. For example, the following allows the user john and the user mary:

```
<Limit READ>
    AllowUser john, mary
</Limit>
```

In contrast, the following code allows the user john but not the user mary. The ! is a logical NOT:

```
<Limit READ>
    AllowUser john, !mary
</Limit>
```

## Miscellaneous Options

The following are some of the common tags that can be used to further define how proftpd works:

- **AllowRetrieveRestart**—This option, when set to on (default), allows clients to resume interrupted file retrievals. It's recommended that you set this option to on.
- **AllowStoreRestart**—This option, when set to on, allows clients to resume interrupted file uploads to the server. We don't recommended that you set it to on because this will allow various users to corrupt existing files. Its default setting is off.
- **CDPath**—This is exactly like the shell's CDPATH environment variable. It takes a path as an argument, allowing the user to directly change her working directory to any directory inside that path by just specifying its name. For example, suppose you have a directory called /usr/local and inside it you have /usr/local/files. Setting CDPath to /usr/local/, as in the following:
  
  ```
  CDPath /usr/local/
  ```
  
  will allow any user to change her working directory to /usr/local/files by just typing the following regardless of where that user is currently positioned on the filesystem:
  
  ```
  cd files
  ```
- **DefaultTransferMode**—ftp uses one of two modes of transfer—ASCII for text files and Binary for others. Usually, ftp clients tell the server which one to use, depending on the type of file being transferred. You can tell proftpd which to use by default just in case. The following is an example:
  
  ```
  DefaultTransferMode binary
  ```
- **HiddenStore**—Setting this option to on will cause proftpd to store incoming files as hidden files until the transfer is complete. When the file is fully transferred, proftpd will unhide it. This is useful if you want to ensure that no one attempts to download a file that is still being uploaded to the server.
- **HideNoAccess**—Entering this option in your configuration file will tell proftpd to hide any directories that the currently logged in user has no permission to see. What is meant by permission here is the Linux filesystem permission. Because the user will be unable to access the directories anyway, you might as well tell proftpd to hide them using this option. This option applies to <Directory> and <Anonymous> sections.
- **MaxLoginAttempts**—This is how many times proftpd will let the user attempt to log in incorrectly before disconnecting him.
- **ShowDotFiles**—Setting this option to on will cause proftpd to show hidden dot files.

# CHAPTER 18 Secure File Transfer Protocol (FTP) Service

> TIP
Although this section of the chapter discusses the use of the standard ftp client, other text-based FTP clients are available for Linux. Nc-FTP, which is included on the Red Hat CD-ROM or www.ncftp.com, gives users extra functionality, such as the ability to get multiple directories in one (without performing recursive mgets and recreating the directory structure on their local machines). The Web site for this product has a list of all features client offers to the user—in addition to the standard set of actions descriptor in the example.

These are some of the commands available during an FTP session. By typing help, the user can see a full list of valid commands. Typing help command-name displays a brief description of what that command does. Listing 18.8 shows the help output.

# LISTING 18.8 The Commands Listed by help in an FTP Session

Commands may be abbreviated. Commands are:

| cr mdir proxy send |
| $ delete mget sendport site |
| account debug mkdir put size |
| append dir mls pwd status |
| ascii disconnect mode quit struct |
| bell form modtime quote system |
| binary get mput recv sunique |
| by glob newer regret tenex |
| case hash nmap rstatus trace |
| ccc help nlist rhelp type |
| cd idle rename user |
| cdup image open reset umask |
| chmod lcd passive restart verbose |
| clear ls prompt rmdir ? |
| close macdef prompt runique |
| cprotect mdelete protect safe |

# A Typical FTP Session Using the ftp Command

When you have configured the server, you will need to test your configuration. A simple test will help ensure that the server is running properly, is responding to FTP requests, and offering the directories and files you want to share.

Begin the test by initiating a connection to the server.

```
$ ftp pheniox
Connected to pheniox.
220 pheniox FTP server (Version uW-2.6.1-18) ready.
Name (phenox:tdc): anonymous
```
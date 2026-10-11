The **unix password sync** statement, if uncommented along with **encrypt passwords**, ensures that the user's login password changes whenever the SMB-encrypted password changes. To accomplish this task, Samba calls the program specified by **passwd program**. The tool specified by the **passwd chat** statement regulates the discussion between the Samba server and the tool set in the **passwd program** statement. *passwd chat* contains the information necessary to answer the **passwd program's** requests. In the preceding code, this exchange begins with the Samba server watching for \*New\*UNIX\*password\*. The asterisks are wildcards that accept any text, the purpose of which is to ignore any formatting or additional language around these three keywords. When the Samba server receives this collection of words, it sends %n, which is the new password, and then finishes by sending the newline character, \n.

After the information is sent, the Samba server waits for *\*ReType\*new\*UNIX\*password\**, once again using wildcards to assure that it is only watching for keywords. When it receives this text, it sends the new password and again sends a newline. The code continues on to the next line. When the server sees *\*password\*all\*authentication\*tokens\*updated\*successfully\**, it knows that all is well and considers the password changed.

The following line begins the code that handles usernames:

```
; username map = /etc/smbusers
```

The **username map** statement points to a file containing data on how to convert usernames from remote machines to this machine. See the Immediate Solutions section “Creating A User Map” for instructions on how to set up one of these map files. The value for this statement is the path to the map file.

You can also set Samba to handle various machines differently, with the following:

```
; include = /etc/smb.conf.%m
```

An **include** statement enables you to insert additional configuration files for particular machines. You can use any substitution method in this statement, except for %u, %P, or %S.

Next is the following line:

```
socket options = TCP_NODELAY SO_RCVBUF=8192 SO_SNDBUF=8192
```

The **socket options** statement sets what *network socket* the Samba server uses to talk to clients. A *socket* is the point through which network clients and servers
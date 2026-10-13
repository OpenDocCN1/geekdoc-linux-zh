```
[-M] [-R] [-S] [-r] [-A] [-h] [-B broadcast address] \
[-U unicast address] [-d debug level] [-s configuration file] \
[-i NetBIOS scope] [-T] name
```

# nmblookup

is used to query NetBIOS names and map them to IP addresses in a network using NetBIOS over TCP/IP queries. The options allow the name queries to be directed at a particular IP broadcast area or to a particular machine. All queries are done over UDP.

# pwdump

will create an smbpasswd file based on contents of Windows NT registry account information.

# smbclient

```
servicename [password] [-s smb.conf] [-B IP addr] \
[-O socket options] [-R name resolve order] [-M NetBIOS name] \
[-i scope] [-N] [-n NetBIOS name] [-d debuglevel] [-P] [-p port] \
[-l log file base] [-h] [-I dest IP] [-E] [-U username] \
[-L NetBIOS name] [-t terminal code] [-m max protocol] \
[-W workgroup] [-T<\c>\IXFqgbNan] [-D directory] \
[-c command string]
```

# smbclient

is a client that can "talk" to an SMB/CIFS server. It offers an interface similar to that of the FTP program, Operations include things like getting files from the server to the local machine, putting files from the local machine to the server, retrieving directory information from the server, and so on.

# smbd

```
[-D] [-a] [-o] [-d debug level] [-l log file] [-p port number] \
[-O socket options] [-s configuration file] [-i scope] [-P] [-h]
```

# smbd

is the server daemon that provides file sharing and printing services to Windows clients. The server provides file space and printer services to clients using the SMB (or CIFS) protocol\&. This is compatible with the LAN Manager protocol, and can service LAN Manager clients. These include MSCLIENT 3.0 for DOS, Windows for Workgroups, Windows 95, Windows NT, OS/2, DAVE for Macintosh, and smbfs for Linux.

# smbpasswd
the account permissions specified by the **admin user**, **guest account**, **force user**, and **force group** parameters. Remember that accounts identified by the **admin user** parameter are running with **root** permissions. Also note that the user name and password will be sent in the clear over the wire if the **encryption** parameter is set to no. More about this in the "Passwords" section below.

```
security = user
```

*Server-level authentication* is similar to user-level authentication. Samba informs the client that user-level authentication is required. The client sends a user name and password in the SMB session setup request. Samba forwards the session setup request to one of the password servers specified in the `password server` parameter. The password server returns the session UID that will be used for the connection. Note that the returned UID must either match or be mapped to a valid UID on the Samba resource servers.

```
security = server
password server = <hostname1 hostname2 ... hostnameN>
```

*Domain-level authentication* indicates that the Samba resource server is participating in a Windows NT domain. The client and server interactions are the same with the exception that NTLM encrypted passwords are required. The session setup request is forwarded to one of the domain controllers identified in the `password server` parameter. As with server authentication the domain user account must match or map to a valid UNIX UID. Domain-level authentication provides additional functionality in that client requests may be validated through trust relationships with other domains.

```
security = domain
encrypt = yes
password server = <pdc-name bdc1-name ... bdcN-name>
```

# User Name Case

Matching user names between UNIX and Windows systems during SMB session setup isn't always as straightforward as one would hope. The problem is that even though you may maintain a consistent set of user names among all your UNIX and Windows systems, many Windows and DOS clients uppercase the user name before submitting it in a session setup request. This can be a problem if you support mixed-case usernames on the Samba server. What this means is that your Samba server has to spend CPU cycles attempting to find a match for the tendered user name by shifting the case of the letters in the string. The default behavior is that Samba will first attempt a match using all lowercase, followed by lowercase with the first letter capitalized. If the match attempt fails, then the connection request is denied. If you've got extra cycles to spare, you can request that Samba try additional combinations of upper/lower case using the `username level` parameter. This parameter accepts a numeric value that determines the number of combinations to try. The higher the number, the more combinations will be tried:

```
username level = <0-5>
```

# Username Mapping
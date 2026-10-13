
*Share level authentication* dictates that clients supply a password associated with the requested resource before a connection is established. Note that there may be more than one password associated with a resource. For example, you might specify separate read-only and read-write passwords for a file share using the `read-list` and `write-list` parameters. Share level does not require a user name and thus does not require an SMB session setup step. If a user name is supplied, it is ignored. If guest access is permitted, the client submits a blank password. Share-level authentication was the default level in Samba releases prior to version 2.0 and for Windows 95 file and printer sharing (Figure 7.1). As of Samba Version 2.0 the default **security** setting is **user** for compatibility with Windows 98 and Windows NT.

```
security = share
```

![](img/7684008b1d7775727df27d44aed5b3f0_98_0.png)

Figure 7.1: Windows 9x security level

*User level authentication* validates a client-supplied username and password against the Samba server's password database.

Once it is authenticated, client access rights to the requested share are governed by the effective UID and GID permissions of the supplied username. The newly spawned `smbd` process for the connection assumes the permissions of the authenticated user name or
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

## User Name Case

Matching user names between UNIX and Windows systems during SMB session setup isn't always as straightforward as one would hope. The problem is that even though you may maintain a consistent set of user names among all your UNIX and Windows systems, many Windows and DOS clients uppercase the user name before submitting it in a session setup request. This can be a problem if you support mixed-case usernames on the Samba server. What this means is that your Samba server has to spend CPU cycles attempting to find a match for the tendered user name by shifting the case of the letters in the string. The default behavior is that Samba will first attempt a match using all lowercase, followed by lowercase with the first letter capitalized. If the match attempt fails, then the connection request is denied. If you've got extra cycles to spare, you can request that Samba try additional combinations of upper/lower case using the `username level` parameter. This parameter accepts a numeric value that determines the number of combinations to try. The higher the number, the more combinations will be tried:

```
username level = <0-5>
```

## Username Mapping

For environments with significant disparity in existing UNIX and Windows namespaces, Samba provides a means of mapping dissimilar usernames between systems. User name mapping can also be used to map multiple user names into a single user name. The many-to-one mapping simplifies file-sharing activities among group members. User name mapping is enabled by specifying the UNIX path name of a file that contains client-to-server user name assignments as a value to the username map global parameter:

```
username map = </path/Filename>
```

Each line in the named mapping file assigns a valid server user name as a match to one or more client user names using an "=" sign character (Example 7.2). A list of client user names which are members of a UNIX group can be designated on the right side of the equation using @groupname syntax. An "*" character can be used as a wildcard to indicate that any user name will match. Lines in the file can be up to 1,023 characters in length. Lines beginning with an "#" or ";" characters are ignored by the parser.

### Example 7.2. Username Mapping

```
Syntax: username = username1 username2 ... usernameN
root = Administrator
wheel = @system
!guest = *
```

Parsing of the map file includes all lines in the file. Any line that begins with an "!" character will terminate parsing if a match was made. Failing a valid match, parsing will continue until the end of the file.

## Passwords

Passwords are the backbone of most UNIX and Windows computer security systems. Therefore, most of us spend a great deal of time fine-tuning and hardening the password infrastructure. This usually means regularly checking password databases for easily guessed passwords, periodically updating password rules and dictionaries, keeping clear-text passwords off the network, schooling users on proper password use, and wrestling with users over general password policy issues. For most, it's a never-ending, thankless job.

None of us wants to increase the complexity of maintaining password services or undermine the security we've worked so hard to put in place. Unfortunately, UNIX and Windows systems don't play by the same rules when it comes to passwords. First, they employ different one-way algorithms for encrypting passwords. LAN Manager servers hash the uppercased password, Windows NT4 stores an MD4 hash of a Unicode version of the password, and UNIX uses crypt(), a modified DES algorithm to encrypt the password with a random salt. To further complicate matters, older Windows systems present uppercased clear-text passwords during session setup. Fortunately, Samba provides a number of options for dealing with the disparity between UNIX and Windows password schemes.

### Clear-Text Passwords

Assuming your network is secure from password sniffing (whose is?), authorizing clear text passwords at SMB session setup time is probably the simplest method for managing
passwords in a mixed UNIX and Windows environment. Conversely, it is the worst method in regard to security. The password presented to Samba by the client is validated against the UNIX password file using standard UNIX authentication methods:

```
encrypt passwords = false
security = <user or share>
```

Along with the security problems associated with clear-text passwords on the wire, you might also experience problems with clients like Windows for Workgroups that may uppercase mixed-case passwords before sending them to the server. Analogous to the previous section on uppercased usernames, Samba supplies a password level parameter that directs the server to try different combinations of upper- and lowercase characters if the uppercase password check fails. The parameter accepts a numeric value that indicates the number of combinations to attempt before giving up. The higher the parameter value, the more character combinations will be tried when validating the password. A value of '0' will direct the server to check all uppercase and all lowercase renditions of the password before denying access.

```
password level = <integer value>
```

Windows NT4 at service pack 3; updated versions of Windows 95; Windows 98; and Windows 2000 all negotiate encrypted passwords only at SMB session setup. To restore support for clear-text passwords either install the appropriate registry updates available in the Samba distribution ./docs directory (Table 7.1) or edit the registry directly using regedit (Example 7.3).

### Table 7.1 Windows Plain Text Password Registry Update Files

| Registry Update File |
|---|
| ./samba <version>/docs/NT4_PlainPassword.zip |
| ./samba <version>/docs/Win2000_PlainPassword.zip |
| ./samba <version>/docs/Win95_PlainPassword.zip |
| ./samba <version>/docs/Win98_PlainPassword.zip |

### Example 7.3 Registry Edit for Plain Text Password Support

### Windows NT

```
Find:HKEY_LOCAL_MACHINE\system\CurrentControlSet /
    \Services\rdr\parameters
Add:    EnablePlainTextPassword, dword:00000001
```

### Windows 9x

```
Find:HKEY_LOCAL_MACHINE\System\Current\ControlSet /
    \Services\VxD\NETSUP
```

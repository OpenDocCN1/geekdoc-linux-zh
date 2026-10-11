**Command Patterns** Along with user-based and host-based authentication, SOCKS5 allows you to selectively specify which commands the client is allowed to execute through the server. Table 10.6 shows the patterns for these commands. Note that, as with authentication methods, you can specify a comma-separated list containing any combination of commands.

Table 10.6 *socks5.conf Command Patterns*

| Pattern | Description |
| :------------- | :--------------------------------------- |
| c | Connect |
| b | Bind |
| u | UDP |
| p | Ping |
| t | Traceroute |
| c, b, p | Multiple commands (any combination) |
| \- | Wildcard (all commands match) |

# The SOCKS5 Password File

It’s always a good idea to have your SOCKS5 clients authenticate themselves using usernames and passwords when traversing a proxy server. To enable this feature, you need to create and maintain a password file on the server. The format of this file is straightforward, with one line of plain text for each user. Each line starts with the username, followed by one or more empty spaces, followed by the password assigned to that user. The following excerpt includes three sample lines in a SOCKS5 password file:

```
alice    myKat_4
bob      $sh0t5
charlie  MandMs
```

Note that, unlike in the standard Linux password files, the SOCKS5 password appears in cleartext; that is, unencrypted and unhashed. In order to minimize the exposure of this password file, no user logins should be allowed on the SOCKS5 server host, and its access should be closely monitored. It’s also important to make sure that this file has the minimum amount of permissions necessary. It only needs to be accessible by the root user for
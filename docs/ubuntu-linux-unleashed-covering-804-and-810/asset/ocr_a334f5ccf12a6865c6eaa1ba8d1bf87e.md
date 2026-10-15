istrator a quick decode of what the conversion rule is doing—that is, uncompressing the file.

# Examples

Several conversion rules may be specified in wu-ftpd’s default ftpconversions file. Additional examples, such as for Sun’s Solaris operating system, might also be available in additional wu-ftpd documentation.

# Using the ftphosts File to Allow or Deny FTP Server Connection

The purpose of the ftphosts file is to allow or deny specific users or addresses from connecting to the FTP server. The format of the file is the word allow or deny, optionally followed by a username, followed by an IP or a DNS address.

```
allow username address
deny username address
```

Listing 18.3 shows a sample configuration of this file.

# LISTING 18.3 ftphosts Configuration File for Allowing or Denying Users

```
# Example host access file
#
# Everything after a '#' is treated as comment,
# empty lines are ignored
allow tdc 128.0.0.1
allow tdc 192.168.101.*
allow tdc insane penguin.net
allow tdc *.exodus.net
deny anonymous 201.*
deny anonymous *.pilot.net
```

The * is a wildcard that matches any combination of that address. For example, allow tdc *.exodus.net allows the user tdc to log in to the FTP server from any address that contains the domain name exodus.net. Similarly, the anonymous user is not allowed to access the FTP if he is coming from a 201 public class C IP address.

```
# /etc/init.d/inetutils-inetd restart
```
# load printers=(G)

This defaults to yes. A yes value loads all printers in printcap for Samba browsing.

# null passwords=(G)

This option defaults to no, meaning no user with a zero-length password on the server can log into Samba. Setting this to yes is an obvious security risk.

# password level and username level (G)

These determine the level of non-case-sensitivity of username and password comparisons. The default is 0, meaning the client-provided password or username is first compared sensitively against the copy on the server, and if the client username or password is converted to lowercase and compared to the copy on the server if that fails.

In troubleshooting Samba connection problems from Windows clients, it's often handy to set these high (such as 24), to see if that fixes the problem. Although this represents a minor security problem and also slows initial connection, it often solves the problem. After problems have been fixed, an attempt should be made to re-comment these two options to beef up security.

Connection problems from Windows clients also are often solved with the encrypt passwords= smb passwd file= options.

# security=(G)

Default is security=user, which enforces security by user and password. This is generally the best choice, with excellent security and predictability.

security=server security=domain are used primarily when password authentication is actually done by yet another machine. security=domain is used to join Samba to a NT domain. security=share offers less security and less predictable operation, but is sometimes a logical choice in less security-intense situations, such as if most of the client usernames do not exist on the server or if most are printers requiring passwords.

This topic is important, and is discussed further in documents /usr/doc/packages/samba/textdocs/security_level.txt and /usr/doc/packages/samba/textdocs/DOMAIN_MEMBER.txt.
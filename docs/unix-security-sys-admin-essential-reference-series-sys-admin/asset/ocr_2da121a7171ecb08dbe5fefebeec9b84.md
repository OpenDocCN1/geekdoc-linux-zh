# Configuration Files

The login process references the files /etc/passwd, /etc/security/passwd, /etc/security/login.cfg, and /etc/security/user. /etc/passwd is the standard UNIX password file, owned by root and world readable. The layout and weakness of the original UNIX password file were explained in Chapter 8 [1, 2, 3, 4]. As a remedy, AIX uses the shadow password file /etc/security/passwd (Figure 9.1), which is owned by root and has read and write permissions for root only.

As shown in Figure 9.1, the second field in /etc/passwd either contains an exclamation mark or is empty, in which case the user has no password. The user ID is used as a key to search for attributes in /etc/security/passwd. The password attribute refers to the encoded password, while lastupdate is the time in epoch (seconds since midnight, 1 January 1970) when the password was last changed. flags contains additional information on password changing and checking [5].

The file /etc/security/login.cfg changed considerably from AIX v3. It is divided into three parts: port configuration, password verification rules, and user definition. The default stanza applies to all ports. Each port can be defined separately and can overwrite the values in the default stanza entry.

Figure 9.2 shows an example of the v4 /etc/security/login.cfg. The first section of login.cfg specifies the default attributes for port definitions. Since most of the attributes are new with this version, I will list each and identify its function.

+   - herald Message printed when port is opened by getty.
+   - logindelay Delay in seconds between unsuccessful logins.
+   - logindisable Number of unsuccessful login attempts before port is closed.

![](bbox=[0.17, 0.85, 0.88, 0.98])
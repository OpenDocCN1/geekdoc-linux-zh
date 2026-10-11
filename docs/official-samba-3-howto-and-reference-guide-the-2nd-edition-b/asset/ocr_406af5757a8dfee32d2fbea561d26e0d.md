traverse access only to the root user and the smbpasswd file itself must be set to be read/write only by root, with no other access.

# **NT Password Hash**

This is the Windows NT hash of the user’s password, encoded as 32 hex digits. The Windows NT hash is created by taking the user’s password as represented in 16-bit, little-endian UNICODE and then applying the MD4 (internet rfc1321) hashing algorithm to it.

This password hash is considered more secure than the LANMAN Password Hash as it preserves the case of the password and uses a much higher quality hashing algorithm. However, it is still the case that if two users choose the same password this entry will be identical (i.e. the password is not “salted” as the UNIX password is).

> WARNING !! Note that, due to the challenge-response nature of the SMB/CIFS authentication protocol, anyone with a knowledge of this password hash will be able to impersonate the user on the network. For this reason these hashes are known as *plain text equivalents* and must NOT be made available to anyone but the root user. To protect these passwords the smbpasswd file is placed in a directory with read and traverse access only to the root user and the smbpasswd file itself must be set to be read/write only by root, with no other access.

# **Account Flags**

This section contains flags that describe the attributes of the users account. In the Samba 2.2 release this field is bracketed by ‘[’ and ‘]’ characters and is always 13 characters in length (including the ‘[’ and ‘]’ characters). The contents of this field may be any of the following characters:

+   * *U* - This means this is a "User" account, i.e. an ordinary user. Only User and Workstation Trust accounts are currently supported in the smbpasswd file.
+   * *N* - This means the account has no password (the passwords in the fields LANMAN Password Hash and NT Password Hash are ignored). Note that this will only allow users to log on with no password if the `null_passwords` parameter is set in the smb.conf(5) config file.
+   * *D* - This means the account is disabled and no SMB/CIFS logins will be allowed for this user.
+   * *W* - This means this account is a "Workstation Trust" account. This kind of account is used in the Samba PDC code stream to allow Windows NT Workstations and Servers to join a Domain hosted by a Samba PDC.

Other flags may be added as the code is extended in future. The rest of this field space is filled in with spaces.

# **Last Change Time**

This field consists of the time the account was last modified. It consists of the characters ‘LCT:’ (standing for "Last Change Time") followed by a numeric encoding of the UNIX time in seconds since the epoch (1970) that the last change was made.
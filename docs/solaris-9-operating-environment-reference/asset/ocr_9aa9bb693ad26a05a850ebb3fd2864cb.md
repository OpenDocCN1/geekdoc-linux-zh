```
castle@ destroy
Tickets destroyed
castle@ ls /mntkrb
Can't get Kerberos key: No ticket file (tf_util)
NSF getattr failed for server castle: RPC: Authentication error
cannotot access directory /mntkrb.
castle@
```

# Files

/tmp/krb5cc_uid
Default credentials cache (uid is the decimal UID of the user).

# Attributes
See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| Availability | SUNMkrbu |

# See Also
kinit(1), klist(1), attributes(5), SEAM(5)

# Authors
Steve Miller, MIT Project Athena/Digital Equipment Corporation; Clifford Neuman,
MIT Project Athena; Bill Sommerfeld, MIT Project Athena

# keylogin — Decrypt and Store Secret Key with keyserv
Synopsis
/usr/bin/keylogin [-r]

Description
The keylogin command is part of the set of RPC commands. Before you use
keylogin, a system administrator must use the newkey(1M), nisaddcred(1M),
niscient(1M) commands to generate a public and secret key. Each user has a unique
public and secret key. The key can be found in the /etc/public key file (see
public(4) in the NIS map publickey.byname, or in the NIS+ table cred.org_dir
/etc/nwitch.conf file (see nsswitch.conf(4)).
The keylogin command prompts for password and uses it to decrypt the user's
secret key. Once decrypted, the secret key is stored by the local key server process,
keyserv(1M). This stored key is used when requests are issued to any secure RPC
services, such as NFS or NIS+. You can delete the key stored by keyserv with the
keylogout(1) command.
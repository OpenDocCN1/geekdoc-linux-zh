Table 2.20 describes the Encryption options available for the SSH server.

**Table 2.20** Options in the Encryption Section (Windows)

| OPTION | DESCRIPTION |
| :--- | :--- |
| Ciphers | Lists the types of cipher-text to be used to encrypt the session. Triple-DES (3DES), Blowfish, ArCFour, Twofish, CAST – 128, and DES are supported. More global options can be set, such as Any, Anystd, anycipher, and anystdcipher. Any and anystd allow standard ciphers; anycipher allows any ciphertext; anystdcipher allows any cipher listed in the IETF SSH draft/A setting of none offers no cipher. |
| MACs | Message Authentication Code (MAC) is a hash algorithm that verifies the integrity of the data before and after transmission. The algorithms supported are SHA1, MD5, SHA1-96, and MD5-96. Multiple MACs can also be set. |
| RekeyIntervalSeconds | Specifies the amount of time before the key-exchange process is executed again. The default is 3600 seconds, which is one hour. The key-exchange process can be disabled by setting the value to zero. |
| RandomSeedFile | Identifies the location of the random seed file. This file is used to generate randomness for the SSH server. |

# ## Users Settings

The Users section of the sshd_2_config file should look like the following:

```
LoginGraceTime				600
PermitRmptyPasswords	no
UserConfigDirectory		"$D\_ssh2"
AuthorizationFile		"authorization"
PrivateWindowStation	yes
```

The User Authentication section of the SSH configuration GUI should look like Figure 2.5.
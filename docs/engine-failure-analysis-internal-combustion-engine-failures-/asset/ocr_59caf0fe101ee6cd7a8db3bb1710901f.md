# **COMMANDS (CONT.)**

| Use This Command | To Do This |
|---|---|
| `-export` [*user ID*] | Export all key rings or those of the specified user ID. |
| `-export-all` [*user ID*] | Export all key rings, or those of the specified user ID, including those that are not compatible with OpenPGP. |
| `-export-ownertrust` | Display the assigned owner trust values. |
| `-export-secret-keys` [*user ID*] | Export all secret keys, or those of the specified user ID. This option poses a security risk and should not normally be used. |
| `-fingerprint` [*user ID*] | List all keys with their fingerprints or those with the specified user ID. |
| `-gen-key` | Launch an interactive utility that generates a new key pair. |
| `-gen-revoke` *user ID* | Generate a complete revocation certificate for the specified user’s user ID. |
| `-h`, `-help` | Display available options. |
| `-import` [*filename*] | Add the keys in the specified filename to the key ring. |
| `-fast-import` [*filename*] |
| `-import-ownertrust` [*filename*] | Update the trust database with the settings specified in *filename*. |
| `-list-keys` [*user ID*] | Show the keys on the specified key ring, or just those owned by the specified user ID. |
| `-list-public-keys` [*user ID*] |
| `-list-secret-keys` [*user ID*] | Show the keys on the specified secret key ring or just those owned by the specified user ID. |
| `-list-sigs` [*user ID*] | Show the keys and signatures on the specified key ring or just those owned by the specified user ID. |
.gnupg directory will also hold encryption files such as secring.gpg for your secret keys (secret keyring), pubring.gpg for your public keys (public keyring), and trustdb.gpg, which is a database for trusted keys.

| GPG Commands | Description |
|---|---|
| -s, --sign | Signs a document, creating a signature. May be combined with --encrypt. |
| --clearsign | Creates a clear text signature. |
| -b, --detach-sign | Creates a detached signature. |
| -e, --encrypt | Encrypts data. May be combined with --sign. |
| --decrypt [file] | Decrypts file (or stdin if no file is specified) and writes it to stdout (or the file specified with --output). If the decrypted file is signed, the signature is verified. |
| --verify [sigfile] [signed-files] | Verifies a signed file. The signature can be either contained with the file or be a separate detached signature file. |
| --list-keys [names] | Lists all keys from the keyrings or those specified. |
| --list-public-keys [names] | Lists all keys from the public keyrings or those specified. |
| --list-secret-keys [names] | Lists your private (secret) keys. |
| --list-sigs [names] | Lists your keys along with any signatures they have. |
| --check-sigs [names] | Lists keys and their signatures and verify the signatures. |
| --fingerprint [names] | Lists fingerprints for specified keys. |
| --gen-key | Generates a new set of private and public keys. |
| --edit-key name | Edits your keys. Use commands to perform most key operations such as sign to sign a key or passwd to change your passphrase. |
| --sign-key name | Signs a public key with your private key. Same as sign in --edit-key. |
| --delete-key name | Removes a public key from the public keyring. |
| --delete-secret-key name | Removes private and public keys from both the secret and public keyrings. |
| --gen-revoke | Generates a revocation certificate for your own key. |
| --export [names] | Exports a specified key from your keyring. With no arguments, exports all keys. |
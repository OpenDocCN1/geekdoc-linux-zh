Table 16-1: GPG Commands and Options

| GPG Commands | Description |
|---|---|
| `--edit-key name` | Edits your keys. Use commands to perform most key operations such as `sign` to sign a key or `passwd` to change your passphrase. |
| `--sign-key name` | Signs a public key with your private key. Same as `sign in --edit-key`. |
| `--delete-key name` | Removes a public key from the public keyring. |
| `--delete-secret-key name` | Removes private and public keys from both the secret and public keyrings. |
| `--gen-revoke` | Generates a revocation certificate for your own key. |
| `--export [names]` | Exports a specified key from your keyring. With no arguments, exports all keys. |
| `--send-keys [names]` | Exports and sends specified keys to a keyserver. The option `--keyserver` must be used to give the name of this keyserver. |
| `--import [files]` | Imports keys contained in files into your public keyring. |
| **GPG Options** | **Description** |
| `-a, --armor` | Creates ASCII armored output, ASCII version of encrypted data. |
| `-o, --output file` | Writes output to a specified file. |
| `--default-key name` | Specifies the default private key to use for signatures. |
| `--keyserver site` | The keyserver to look up public keys not on your keyring. Can also specify the site to send your public key to. `host -l pgp.net | grep www.keys` will list the keyservers. |
| `-r, --recipient names` | Encrypts data for the specified user, using that user's public key. |
| `--default-recipient names` | Specifies the default recipient to use for encrypting data. |

# GnuPG Setup:gpg

Before you can use GnuPG, you will have to generate your private and public keys. On the command line (terminal window), enter the `gpg` command with the `--gen-key` command. The `gpg` program will then prompt you with different options for creating your private and public keys. You can check the `gpg` Man page for information on using the `gpg` program.

```
gpg --gen-key
```

# Creating Your Key

You are first asked to select the kind of key you want. Normally, you would just select the default entry, which you can do by pressing the ENTER key. Then you choose the key size, usually the default 1024. You then specify how long the key is to be valid-usually, there is no expiration. You will be asked to enter a user
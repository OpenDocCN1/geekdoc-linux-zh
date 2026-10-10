example, while OpenSSH uses “-i <privatekey>” syntax, SSH Communications' uses “-i identification” for the syntax. The syntax to create the identification file is as follows on the client:

```
```
echo *IdKey SSH2-Shreya* >> identification
```
```

+   4. After the identification file has been created on the SSH server, the permissions on the public-key and private-key pairs need to be protected in order to be used. Set the following permission on the SSH client for the appropriate key files that were generated.

```
```
[Shreya@localhost]$chmod 600 SSH2-Shreya
[Shreya@localhost]$chmod 600 SSH2-Shreya.pub
```
```

+   5. Once you have made the key pairs, uploaded the public-key files to the appropriate home directory, added the entry to the authorization file, and added the entry to the identification file, you should now be able to log in with the public key. Be sure to use the identification file with the `-i` option, not the private-key file; otherwise you will receive a “No further authentication methods available” error. The following is sample syntax:

```
```
[Shreya@localhost]$ssh2 SSH-Server -i identification
```
```

# ## How to Use an OpenSSH Key on a VShell SSH Server

Using an OpenSSH client key for a VShell SSH server is more straightforward than the previous section. Since VShell SSH servers accept the OpenSSH key format, it is not necessary to convert OpenSSH keys to any other format, which saves valuable time and a lot of potential headache! Since you have an OpenSSH client key, I will demonstrate how to use the OpenSSH key for VShell SSH servers.

+   1. Copy the OpenSSH public-key file to the remote VShell SSH server, specifically in public-key folder located at C:\ Program Files\VShell\PublicKey\%USER%.

+   2. Make sure public-key authentication is enabled on the remote VShell SSH server.

+   3. From the client machine, connect to the VShell SSH server with the following syntax:

```
```
ssh <VShell Server> -P 22 -i OpenSSHPrivateKey -l <username on VShell server>
```
```
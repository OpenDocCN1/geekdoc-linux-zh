accepts the OpenSSH key format; therefore, the converted OpenSSH key from the previous section could also be used on a VShell SSH server. I will now demonstrate how to use both an SSH Communications' SSH key and a converted OpenSSH client key for VShell SSH servers.

+   1.  Copy your SSH Communications' key and OpenSSH public key-file to the remote VShell SSH server, specifically in public-key folder located at C:\ Program Files\VShell\PublicKey\%USER%.
+   2.  Make sure public-key authentication is enabled on the remote VShell SSH server.
+   3.  From the client machine, connect to the VShell SSH server with the following syntax.

```
ssh2 <VShell Server> -p 22 -i identification -1 <username on VShell server>
ssh <VShell Server> -p 22 -i OpenSSHPrivateKey -1 <username on VShell server>
```

Using the previous example, with id_dsa_2048_a and the SSH Communications' key and id_dsa_2048_a_Open as the converted OpenSSH client key, complete the following steps to authenticate to the VShell SSH server.

# SSH Communications' Client Key

```
ssh2 VshellServer -p 22 -i identification -1 <username>
Enter passpharse for key '<username>':
Authenticated with partial success
Shreya@VshellServer's password:
C:\
```

# OpenSSH Convert Client Key

```
ssh VshellServer -p 22 -i id_dsa_2048_a_Open -1 <username>
Enter passpharse for key '<username>':
Authenticated with partial success
Shreya@VshellServer's password:
C:\
```

Notice that after the key is authenticated, VShell asks for a password on the VShell server. This happens only if both the password and public-key check-boxes are required on the VShell server. If public key was the only required authentication method, a password prompt would not occur; however, this is a great method of enforcing two-factor authentication, which should be required for management purposes.
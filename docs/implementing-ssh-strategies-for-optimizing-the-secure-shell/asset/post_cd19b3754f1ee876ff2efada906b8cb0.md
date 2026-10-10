
Settings/`<username>`/Application Data/SSH/UserKeys. The following shows the Windows location:

```
Private key saved to C:\Documents and Settings\Administrator\Application Data\SSH\UserKeys\id_dsa_2048_a
Public key saved to C:\Documents and Settings\Administrator\Application Data\SSH\UserKeys\id_dsa_2048_a.pub
```

5. The SSH Communications’ SSH client keys have been generated!

After the creation process has been completed, copy the SSH public-client key to the SSH server. The following section demonstrates how to use SSH client keys with a SSH Communications’ SSH Server, an OpenSSH server, and a VanDyke VShell SSH server.

### How to Use SSH Client Keys with SSH Communications’ SSH Server

After you have securely uploaded your public key (for example, id_dsa_2048_a.pub) to the SSH server, typically in the users’ home directory ( /home/`<username>`/.ssh2 for Unix and Documents and Settings\`<username>`\.ssh2 for Windows), you also need to add a public-key entry to the authorization file, which is labeled Authorization, also in the users’ home directory. The syntax is as follows:

```
Key id_dsa_2048_a.pub
```

After the authorization file has been created on the SSH server, an identification file needs to be created on the SSH client, typically in the ssh2 folder in the users’ home directory ( /home/`<username>`/.ssh2 for Unix and Documents and Settings\`<username>`\.ssh2 for Windows). This file is used by the SSH client, with the `-i` flag, to indicate the private keys to use in order to authenticate. Be sure to use this file with the `-i` option on the SSH client. The syntax to create this file is as follows:

```
echo "idkey id_dsa_2048_a" >> identification
```

Once you have made the key pairs, uploaded the public-key files to the appropriate home directory, added the entry to the authorization file, and added the entry to the identification file, you should be able to log in with the public key. The following is a demonstration of the syntax:

```
ssh2 <SSH server IP address> -i identification
```

### How to Use SSH Client Keys with an OpenSSH Server

To use the SSH Communications’ SSH Client public-key and private-key pair with an OpenSSH server, complete the following steps.

- Make sure your key pairs do not contain a passphrase. While it is important to remove any passphrases during the conversion process, make sure you add a passphrase to both the old key and the newly converted keys after the conversion process is completed. To change the passphrase of your key, use the -e switch.
  ```
  ssh-keygen2 -e id_dsa_2048_a
  ```
- Once the passphrases have been removed, we must convert our SSH Communications’ SSH keys to the OpenSSH compatible format, using the following commands:
  ```
  [Shreya@localhost]$ssh-keygen2 -i id_dsa_2048_a.pub > id_dsa_2048_a_Open.pub
  [Shreya@localhost]$ssh-keygen2 -i id_dsa_2048_a > id_dsa_2048_a_Open
  ```
- Once you have copied the public key to the SSH server, using SFTP or some alternative secure method (there is no automated tool to do this), enter the following command on the OpenSSH server to add the newly converted public key to the authorized key file, located in the users’ home directory, on the OpenSSH server.
  ```
  [Shreya@OpenSSHserver]$cat id_dsa_2048_a_Open.pub >> /home/Shreya/.ssh/authorized_keys
  ```
- On the SSH client, the permissions on the public-key and private-key pairs need to be protected to be used. Set the following permission on the key files that were generated:
  ```
  [Shreya@localhost]$chmod 600 id_dsa_2048_a_Open.pub
  [Shreya@localhost]$chmod 600 id_dsa_2048_a_Open
  ```
- You should now be able to authenticate, since you have converted your SSH Communications’ SSH client key to OpenSSH format and have added the key to the authorized key-list file:
  ```
  /usr/bin/ssh SSH-Server -i id_dsa_2048_a_Open
  ```

### How to Use SSH Client Keys with a VShell SSH Server

Using a SSH Communications’ client key for a VShell SSH server is quite simple. Since VShell SSH servers accept the SSH Communications’ SSH2 key format, it is not necessary to convert SSH Communications’ keys to any other format, which saves valuable time and a lot of potential headache! VShell accepts the OpenSSH key format; therefore, the converted OpenSSH key from the previous section could also be used on a VShell SSH server. I will now demonstrate how to use both an SSH Communications' SSH key and a converted OpenSSH client key for VShell SSH servers.

1. Copy your SSH Communications' key and OpenSSH public key-file to the remote VShell SSH server, specifically in public-key folder located at C:\Program Files\VShell\PublicKey\%USER%.
2. Make sure public-key authentication is enabled on the remote VShell SSH server.
3. From the client machine, connect to the VShell SSH server with the following syntax.

```
ssh2 <VShell Server> -p 22 -i identification -l <username on VShell server>
ssh <VShell Server> -p 22 -i OpenSSHPrivateKey -l <username on VShell server>
```

Using the previous example, with id_dsa_2048_a and the SSH Communications' key and id_dsa_2048_a_Open as the converted OpenSSH client key, complete the following steps to authenticate to the VShell SSH server.

#### SSH Communications' Client Key

```
ssh2 VshellServer -p 22 -i identification -l <username>
Enter passphrase for key '<username>':
Authenticated with partial success
Shreya@VshellServer's password:
C:\
```

#### OpenSSH Convert Client Key

```
ssh VshellServer -p 22 -i id_dsa_2048_a_Open -l <username>
Enter passphrase for key '<username>':
Authenticated with partial success
Shreya@VshellServer's password:
C:\
```

Notice that after the key is authenticated, VShell asks for a password on the VShell server. This happens only if both the password and public-key check-boxes are required on the VShell server. If public key was the only required authentication method, a password prompt would not occur; however, this is a great method of enforcing two-factor authentication, which should be required for management purposes.

### Creating Keys with SSH Communications (Windows GUI)

To create keys the SSH Communications' SSH client, the following steps should be completed.

1. Open the SSH client: Start Programs SSH Secure Shell Secure Shell client.
2. From the Menu bar, select Edit Settings.
3. In the Settings display, there should be a User Authentication section. Under the User Authentication section, there is a subcategory called Keys. Select the Keys subcategory.
4. At this point, you should see a screen similar to Figure 4.8.
5. To generate a new public and private-key pair, select the option that says Generate New…
6. The wizard should be displayed, describing the process of creating a key pair. After you have read the description, select Next.
7. The Key Properties screen should appear next. This screen gives you the option of selecting a DSA or RSA key type and the key length you would like to use. In general, the better the key length, the stronger the security; however, the greater the performance hit you will have to accept. After selecting the type of key and the key length, select Next.
8. The Generation screen should appear next. This screen initiates the process of actually creating the key. The key-generation process can take several minutes. Once the process is completed, select Next.
9. The Enter Passphrase screen should appear next. This screen allows you to enter a name for the public and private-key pair, a comment for description purposes only, and a passphrase to protect the private key. Enter your preferred file name, such as your username, a comment, and a passphrase that is difficult to guess but easy to remember. After entering this information, select Next. (Note that if the passphrases do not match, the Next option will not be enabled. Make sure your passphrases match before attempting to select Next.)
10. The Finish screen should appear next. At this stage, the public and private keys have been generated and stored to your local machine. At this point, you have the option of uploading your public key to the SSH server if a valid connection currently exists. If a valid connection exists (meaning you connected to the SSH server before starting the key-generation procedure), select Upload Public Key; however, you will be uploading the key to multiple SSH servers later in this section, so select Finish and skip to Step 13 if you wish to skip this step.


8. The location screen should appear next. Unless you have a particular area to store the keys, it is recommended to key in the default location (C:\Documents and Settings\Administrator\Application Data\VanDyke\Identity); however, make sure to place NTFS permissions in the folder to restrict access to Guests, Everyone, and other unauthorized groups. After selecting the location, click Finish.
9. You should see a pop-up box, asking if you would like to use the key as your global public key. Select No, since you may have multiple keys with one default global key.
10. VanDyke SecureCRT public and private-key pairs have been generated!
After the creation process has been completed, the process of uploading the public key is next. The following section demonstrates how to upload a SecureCRT client public and private-key pairs to a VanDyke V$shell SSH server, a SSH Communications' SSH server, and an OpenSSH server.

# V$Shell SSH Server

Using a SecureCRT public and private-key pair on VanDyke Software's SSH server is quite simple. The following steps should be complete.

1. Open SecureCRT (Start > Programs > Secure CRT > Secure CRT).
2. Make a valid connection to the V$Shell SSH server using the Quick Connection option.
3. Once a valid connection has been established, go back to the quick connect menu (File > Quick Connect). Under the authentication section, there should be two drop-down boxes. The Primary method should be Password. For the Secondary methods, choose PublicKey and select the Properties button to the right.
4. The Public Key Properties menu should appear. Make sure the Use global public key setting radio button is selected and the Use identity file radio button is also selected. After you have confirmed this, select the ... button and browse to the location of your public key; then select the public-key file.
5. After you have selected your public-key file, select the Upload button to upload the public key to the V$Shell SSH server.
6. When SecureCRT has established a connection, it will ask you to authenticate using your username and password on the V$Shell SSH server. Enter the valid username and password and select OK.
7. Once the username and password are authenticated, the public key will be uploaded to the V$Shell SSH server. You should see a menu similar to Figure 4.13.

![](img/c99d6f526a5f9fa62f2c34daada85ad7_178_0.png)

**Figure 4.13** The confirmation of the SecureCRT public-key upload process.

8. You should now be able to use your public key to authenticate. To confirm, enable only public-key authentication on the V$Shell SSH server.
    a. Select Start > Programs > V$Shell > V$Shell.
    b. Highlight the Authentication section.
    c. Uncheck Password and check Public key for the required authentication methods. Be sure to uncheck the Allow 3 password attempts checkbox, since the public key is already on the V$Shell SSH server.
9. On SecureCRT, select PublicKey for the Primary authentication method and <None> for the Secondary authentication method. Be sure to browse to the correct public key with the Properties button.
10. Select Connect and you will authenticate with your public key and then receive a V$Shell SSH session.

# OpenSSH

To use the SecureCRT Client public and private-key pair for an OpenSSH server, complete the following steps.

1. Make sure your key pairs do not contain a passphrase. While it is important to remove any passphrases during the conversion process, make sure you add a passphrase to both the old key and the newly converted keys after the conversion process is completed.
    a. Go to Start > Programs > SecureCRT > SecureCRT.
    b. Choose File > Quick Connect > Protocol (ssh2) > Authentication (Public Key).
    c. Select Properties > Change Passphrase.
    d. Enter the current passphrase, and leave the new passphrase blank.
    e. Select OK.
2. Once the passphrases have been removed, you must convert your SecureCRT keys to the OpenSSH compatible format. On the client machine, use OpenSSH's ssh-keygen utility to convert the keys. The keys are located at Documents and Settings\<username>\Application Data\VanDyke. Use the following commands:

```text
ssh-keygen -i -f CRTPublickey.pub > CRTPublickeyOpen.pub
ssh-keygen -i -f CRTPriatekey > CRTPriatekeyOpen
```

3. Once you have copied the public key to the SSH server, using SFTP or some alternative secure method, enter the following commands to send the newly converted public key to the authorized key files on the SSH server.

On the OpenSSH server:

```text
cat CRTPublickeyOpen.pub >> authorized_keys
```

4. You should now be able to authenticate, since you have converted your SecureCRT client key to OpenSSH format and have added the key to the authorized key-list file:

```text
/usr/bin/ssh OpenSSH-Server -i CRTPriatekeyOpen
```

# SSH Communications' SSH Server

The process of converting a SecureCRT client key to a SSH Communications' SSH server is more straightforward than the previous section. Since SSH Communications' uses SSH2 keys, converting your SecureCRT key is not required for SSH Communications' SSH servers. Since you have an SSH2 key with your SecureCRT key, I will now demonstrate how to use the SecureCRT key for SSH Communications' SSH servers.

1. Copy your SSH2 SecureCRT public-key file to the SSH Communications' SSH Server, specifically in the .ssh2 folder in the Documents and Settings\<username> directory.
2. Open or make a file named ‘authorization’ located in the following directory; Documents and Settings\<username>\.ssh2. Add the new SecureCRT public key to the authorized key lists.

Key    CRTPublickey.pub

Where CRTPublickey.pub is the SSH2 SecureCRT public key.
3. On the SSH SecureCRT client, open the Quick Connect screen (File > Quick Connect), and enter the following information.
    a. Protocol: ssh2
    b. Hostname: <remote SSH Communications' SSH server>
    c. Port: port number, typically 22
    d. Username: Username of the remote SSH server
    e. Authentication
        - Primary: PublicKey
            - Properties: Use your identity file: c:\Documents and Settings\<username>\Application Data\VanDyke\CRT\publickey.pub
        - Secondary: Password
4. Select Connect.
5. You should now be logged in to a SSH Communications’ SSH server using a SSH2 key generated from SecureCRT.

While the use of public keys for authentication purposes is by far the better solution than password authentication, the process of making SSH client keys interoperate with various SSH servers may not be an easy process in an enterprise environment. For optimal usage, it is better to use tools and utilities that are interoperable with various platforms and technologies, and SSH is no different. The use of V$Shell SSH servers has a significant advantage, since it accepts both OpenSSH keys and SSH2 keys without any need for any conversion from any client mentioned in this chapter. Similarly, using OpenSSH keys as your primary key may be a good solution, since both OpenSSH and V$Shell servers accept the OpenSSH format, leaving only one conversion required to work with SSH2 servers. Nevertheless, the choice of the SSH client-key format and SSH servers will depend on many items, not just the public-key conversion process. As best practice, it is a good idea to have both formats of your public key made: one for OpenSSH and another for SSH2 formats.

# SSH Agents

The SSH agent is a simple utility that allows end-users to handle passphrases attached to public-key files in a simpler way. If multiple passphrases are being used with multiple public keys, it may be cumbersome for the end-user to type and retype all the passphrases several times. The SSH agent utility remembers your passphrases for you after the first time you have authenticated with the passphrase. It is a utility that remembers your private keys and provides the authentication portion to other SSH connections. Therefore, after you initially authenticate with your passphrase, the SSH agent will prevent subsequent SSH sessions from asking you for your passphrase. The process to enable SSH agents involves the following four steps:

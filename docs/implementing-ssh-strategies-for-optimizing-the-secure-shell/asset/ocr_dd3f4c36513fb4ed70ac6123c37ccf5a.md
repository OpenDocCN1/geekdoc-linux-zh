+   2. Once the passphrases have been removed, you must convert your SecureCRT keys to the OpenSSH compatible format. On the client machine, use OpenSSH's ssh-keygen utility to convert the keys. The keys are located at Documents and Settings\<username>\Application Data\VanDyke. Use the following commands:
+   
+   ```text
+   ssh-keygen -i -f CRTPublickey.pub > CRTPublickeyOpen.pub
+   ssh-keygen -i -f CRTPriatekey > CRTPriatekeyOpen
+   ```
+   
+   3. Once you have copied the public key to the SSH server, using SFTP or some alternative secure method, enter the following commands to send the newly converted public key to the authorized key files on the SSH server.
+   
+   On the OpenSSH server:
+   
+   ```text
+   cat CRTPublickeyOpen.pub >> authorized_keys
+   ```
+   
+   4. You should now be able to authenticate, since you have converted your SecureCRT client key to OpenSSH format and have added the key to the authorized key-list file:
+   
+   ```text
+   /usr/bin/ssh OpenSSH-Server -i CRTPriatekeyOpen
+   ```

# **SSH Communications' SSH Server**

The process of converting a SecureCRT client key to a SSH Communications' SSH server is more straightforward than the previous section. Since SSH Communications' uses SSH2 keys, converting your SecureCRT key is not required for SSH Communications' SSH servers. Since you have an SSH2 key with your SecureCRT key, I will now demonstrate how to use the SecureCRT key for SSH Communications' SSH servers.

+   1. Copy your SSH2 SecureCRT public-key file SSH Communications' SSH Server, specifically in the .ssh2 folder in the Documents and Settings\<username> directory.

+   2. Open or make a file-name ‘authorization’ located in the following directory; Documents and Settings\<username>\.ssh2. Add the new SecureCRT public key to the authorized key lists.
+   
+   Key    CRTPublickey.pub
+   
+   Where CRTPublickey.pub is the SSH2 SecureCRT public key.

+   3. On the SSH SecureCRT client, open the Quick Connect screen (File Quick Connect), and enter the following information.

+   a. Protocol: ssh2

+   b. Hostname: <remote SSH Communications' SSH server>
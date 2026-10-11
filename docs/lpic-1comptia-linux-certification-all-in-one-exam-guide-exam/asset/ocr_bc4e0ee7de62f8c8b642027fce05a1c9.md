If, on the other hand, the authorized _keys file does already exist, it's very important that you remember to use the >> redirection characters instead of >. Remember, using >> will append the output of the command to the end of the specified file. Using a single redirection > character will overwrite the entire file with the output of the command. That wouldn't be a good thing if the authorized _keys file already had several keys in it that you wanted to keep.

You can now test the configuration to see if public key authentication works. If you're still logged in to an SSH session with the SSH server, exit out of it. Then establish a new SSH session with the server. You should be prompted for the key file's passphrase instead of a username and password, as shown in Figure 18-9.

Once you enter the passphrase, you will be authenticated to the SSH server. Notice in the next example that no password was requested to establish the SSH session:

```
rtracy@ws1:~$ ssh -l rtracy ws3
Last login: Thu Jun 2 16:13:39 2011 from 192.168.1.84
rtracy@WS3:~>
```

If desired, you can use the ssh-agent command to eliminate the need to enter the passphrase every time you establish an SSH connection. Complete the following:

+   1. At the shell prompt of your client system, enter ssh-agent bash.
+   2. At the shell prompt, enter ssh-add ~/.ssh/id_rsa or ssh-add ~/.ssh/id_dsa, depending upon which key file you have created.
+   3. When prompted, enter the key file's passphrase. When you do, you should be prompted that the identity that has been added. An example follows:

```
rtracy@ws1:~$ ssh-agent bash
rtracy@ws1:~$ ssh-add ~/.ssh/id_rsa
Enter passphrase for /home/rtracy/.ssh/id_rsa:
Identity added: /home/rtracy/.ssh/id_rsa (/home/rtracy/.ssh/id_rsa)
rtracy@ws1:~>
```

Once done, the ssh-agent process stores the passphrase in memory. It then listens for SSH requests and automatically provides the key passphrase for you when requested. Let's practice configuring SSH to use public key authentication in the following exercise:

![](bbox=[0.12, 0.72, 0.35, 0.95])

![](bbox=[0.4, 0.72, 0.9, 0.95])
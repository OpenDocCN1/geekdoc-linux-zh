# Chapter 18: Using Encryption

![](bbox=[0.05, 0.05, 0.25, 0.15])

![](bbox=[0.25, 0.05, 0.92, 0.17])

> **TIP** Don’t forget the -l parameter. If you don’t, the SSH client will attempt to authenticate you to the remote system using the same credentials you used to authenticate to the local system. If the credentials are the same on both the client and server systems, you’ll still be able to authenticate. But if they aren’t, then you won’t be able to authenticate.

For example, if I wanted to connect to a remote Linux system with a hostname of WS3 (which has an IP address of 192.168.1.125) as the user tracy using the ssh client on a local computer system, I would enter `ssh -l tracy WS3` at the shell prompt. This is shown in Figure 18-5.

Notice in Figure 18-5 that I was prompted to accept the public key from WS3 because this was the first time I connected to this particular SSH server. Once done, I was authenticated to the remote system as the tracy user (notice the change in the shell prompt). At this point, I have full access to the shell prompt on WS3 and I can complete any task that I could if I were sitting right at the console of the remote system. To close the connection, just enter `exit` at the shell prompt.

> **TIP** Windows workstations don’t provide an ssh client. You can download the PuTTY.exe ssh client from the Internet and use it to connect to a Linux SSH server from a Windows workstation.

Let’s practice working with SSH in the following exercise.

![](bbox=[0.05, 0.65, 0.22, 0.78])

```
tracy@WS1:~$ ssh -l tracy ws3
The authenticity of host 'ws3 (192.168.1.125)' can't be established.
RSA key fingerprint is 44:31:21:06:37:21:63:38:90:77:08:10:35:74:97:85.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'ws3,192.168.1.125' (RSA) to the list of known hosts
Password:
Last login: Mon May 16 15:52:49 2011
tracy@WS3:~$ 
```
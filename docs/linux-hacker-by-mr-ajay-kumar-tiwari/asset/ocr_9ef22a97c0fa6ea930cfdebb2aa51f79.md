# Linux Hack

Ajay Kumar Tiwari

on the keyfile.

```
Are you sure you want to continue connecting (yes/no)? Yes
Host key saved to
/home/jsmith/.ssh2/hostkeys/key_22_remotehost.example.com.pub
host key for remotehost.example.com, accepted by jsmith Mon
May 26 2008 16:06:50 -0700
jsmith@remotehost.example.com password:
remotehost.example.com$
```

The Second time when you login to the remote host from the localhost, it will prompt only for the password as the remote host key is already added to the known hosts list of the ssh client.

```
localhost$ ssh -l jsmith remotehost.example.com
jsmith@remotehost.example.com password:
remotehost.example.com$
```

For some reason, if the host key of the remote host is changed after you logged in for the first time, you may get a warning message as shown below.

This could be because of various reasons such as:

+   - Sysadmin upgraded/reinstalled the SSH server on the remote host
- Someone is doing malicious activity etc.,

The best possible action to take before saying “yes” to the message below, is to call your sysadmin and identify why you got the host key changed message and verify whether it is the correct host key or not.

```
localhost$ ssh -l jsmith remotehost.example.com
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@WARNING: HOST IDENTIFICATION HAS CHANGED!@
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-
```
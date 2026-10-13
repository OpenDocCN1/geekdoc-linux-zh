# LAB ANSWERS

# Lab 1

This lab should give you an idea of what can be done with /etc/sysconfig files, and how it changes the way a daemon is started. It should also demonstrate the risks; the wrong change, such as that demonstrated in the lab, means that the service won’t work.

# Lab 2

There are three measures of success in this lab.

+   1. There will be an id_rsa file and an id_rsa.pub file in the client /home/hawaii/.ssh directory.
+   2. You'll be able to connect to the remote system without a password. Just enter the "I love Linux!" passphrase when prompted.
+   3. You'll find the contents of the client's id_rsa.pub file in the remote authorized_keys file in the /home/hawaii/.ssh directory.

# Lab 3

Much as in Lab 2, there are three measures of success in this lab.

+   1. There will be an id_dsa and an id_dsa.pub file in the client /home/tonga/.ssh directory.
+   2. You'll be able to connect to the remote system without a password. Just enter the "I love Linux!" passphrase when prompted.
+   3. You'll find the contents of the client's id_dsa.pub file in the remote authorized_keys file in the /home/hawaii/.ssh directory.

# Lab 4

The simplest way to implement this lab is to add the following directive to the /etc/ssh/sshd_config file:

```
AllowUsers hawaii
```

Just don’t forget to reload or restart the SSH service after making the change; otherwise, other users will still have access.

In case you’re curious, user tonga on the client is still able to access the hawaii account on the SSH server with the passphrase, as it is connections to the user hawaii account that are being allowed. The identity of the remote account does not matter to the AllowUsers directive.
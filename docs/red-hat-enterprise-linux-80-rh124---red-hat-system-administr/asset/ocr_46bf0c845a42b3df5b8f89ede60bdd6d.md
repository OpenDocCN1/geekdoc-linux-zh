+   6. Use the ssh-keygen command to generate another set of SSH keys with passphrase-protection. Save the key as /home/operator1/.ssh/key2.

> > WARNING
If you do not specify the file where the key gets saved, the default file (/home/user/.ssh/id_rsa) is used. You have already used the default file name when generating SSH keys in the preceding step, it is vital that you specify a non-default file, the existing SSH keys will be overwritten.

```
[operator1@serverb ]$ ssh-keygen -f .ssh/key2
Generating public/private key pair.
nEnter passphrase (empty for no passphrase): redhatpass
Enter same passphrase again: redhatpass
Enter identification has been saved in .ssh/key2.
Your public key has been saved in .ssh/key2.pub.
The key fingerprint is:
SHA256:0CtjFpSmRbbgbEIWCwAI40S1MEbgRbQ1HWKI
operator1@serverb.lab.example.com
The key's image is:
+----RSA 2048]----+
| 0x* |
| 0B= |
|E0* |
|B000 |
| .= 0 S |
| +.0 0 |
|+.0+ 0 |
|+.0+. |
|!+. -6- |
+----[SHA256]----+
```

+   7. Use the ssh-copy-id command to send the public key of the passphrase-protected key to operator1 ona.

```
[operator1@serverb ]$ ssh-copy-id -i .ssh/key2.pub operator1@servera
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: ".ssh/key2.pub"
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter
out out that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted
now is to install the new keys
```

Number of key(s) added: 1

Now try logging into the machine, with: "ssh operator1@servera"
and check to make sure only the key(s) you wanted were added.

Notice that the preceding ssh-copy-id command did not prompt you for a passwordecause it used the public key that you exported to servera in the preceding step.
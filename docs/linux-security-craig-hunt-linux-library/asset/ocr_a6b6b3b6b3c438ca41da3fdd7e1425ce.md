Third and finally, you need to create an initial secret for each of the users that you want to authenticate via OPIE using the opiepasswd utility. You can set an initial password for them as root. In the following example, you use the `-c` option to signal that you are in a secure terminal (you should only set passwords on the system console). You also specify the `-n 15` option to force opiepasswd to generate 15 one-time passwords for username alice:

```
```
[ramon]$ sudo opiepasswd -c -n 15 alice
Adding alice:
Only use this method from the console; NEVER from remote. If you are using telnet, xterm, or a dial-in, type ^C now or exit with no password.
Then run opiepasswd without the -c parameter.
Using MD5 to compute responses.
Enter new secret pass phrase:
Again new secret pass phrase:
ID alice OTP key is 15 re6667
BEER HANG ONTO DEAD WEAR DANE
```
```

Alternatively, you may want to rely on your users to set their own passwords:

```
```
[alice]$ opiepasswd -c -n 15
Adding alice:
Only use this method from the console; NEVER from remote. If you are using telnet, xterm, or a dial-in, type ^C now or exit with no password.
Then run opiepasswd without the -c parameter.
Using MD5 to compute responses.
Enter new secret pass phrase:
Again new secret pass phrase:
ID alice OTP key is 15 re6667
BEER HANG ONTO DEAD WEAR DANE
```
```

This is the same command as the one from the previous example, but since user alice executes it herself, she does not need root privileges.
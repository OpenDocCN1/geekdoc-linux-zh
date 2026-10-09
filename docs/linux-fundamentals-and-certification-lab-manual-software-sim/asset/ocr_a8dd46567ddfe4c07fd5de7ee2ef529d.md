Users should not repeat passwords. Some users may have two or three passwords that they rotate. This consistency can lead to easy cracking of passwords.

Never use the same password on several different machines. If one machine is compromised, your account on all the machines may be compromised.

**Testing Passwords**

As an administrator, you may want to test the passwords of your users. The best test is to see if you can crack the passwords. There are many password cracking programs that run under Linux, Windows, Unix, and Apple McInthos. Two common programs are:

+   *   **John the Ripper** This password cracker is available for a number of operating systems. Its purpose is to detect weak Linux passwords. It takes a password or shadow password file as input and returns the usernames and passwords discovered.
*   **Crack** This password cracker is one of the oldest and probably the fastest. It is available for Linux systems.

![](bbox=[0.26, 0.31, 0.94, 0.41])

The following is a copy of a shadow password file. Users jsmit h, rbrown, and ksmith have passwords equal to their IDs. Users dengle and davidengle both used strong passwords and were not cracked. User myuser was cracked after about ten minutes.

```
dengle:$1$Rafj$SG$Iftf/8Shq$jIsV9kNo5Vc/:12307:0:99999:7:::
jsmith:$1$k1Kp8$Oxg$aRnLX6/Bvy$7t848ho5flU/:12364:0:99999:7:::
myuser:$1SV3$9bpk.r$f674RsoaH$GmyhWHPC9$8k1:12348:0:99999:7:::
guest::!:12348:0:99999:7:::
davidengle:$1$Px$99kZ$XV$HbSOSuF$739MCD$3XVgh$5k0:12348:0:99999:7:::
rbrown:$1$W$duIYNY$PV$KWHMxz$W/Dcb$YzP.7FWvh.:12364:0:99999:7:::
ksmith:$1$7$hNnA$ThO$R4YgaCArv9R4$j85GY$2HE.:12364:0:99999:7:::
```

The DOS version of John the Ripper was used to crack the passwd file. The file was copied from the server to a file named passwd.txt in a Windows directory.

```
F:\john\JOHN-16\RUN>john passwd.txt
Loaded 6 passwords with 6 different salts (FreeBSD MD5 [32/32])
jsmith   (jsmith)
rbrown   (rbrown)
ksmith   (ksmith)
```

# Administrative Control

Never run a Linux system as root. The root login has full control of the operating system, and an accidental command can have serious consequences. Nevertheless, on any system, there is a need to execute programs with the root user privileges. One way to enable users to execute root commands safely is through a setuid program such as sudo or su. A setuid program operates with the user ID of the owner of the program rather than that of the user operating the program.

**Disable Root Login** You can disable root logins using the /etc/security file. This file lists ttys from which root may log in to the Linux operating system. The /etc/security file is a list of available login devices. To disallow root log in, just remove the entries from the file. Typically, the only login device for the root user is console. An easy way to remove all the entries is with the echo > /etc/security command.
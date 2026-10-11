```
619374038515642525995896839408208733045515172702470073209042978615
060322444446644529326292l876776658946288815292526320347023048092384
080921427992348792734979234701 hontanon@caldera.example.com
```

```
1024 35 239048023495285104318364350181929090082244038957726458073723
565897353708317804367538174812197037594693987194l8848857474810l78479
54020737l6338624148l285585501347l3088523618l26l6l60458988l194l99349l
027939235137895964935l038996402419l71l520040453399005458087l2560344ll
802109537l6628465097l8l09183l89 ramon@redhat.example.com
```

Note that you use two different usernames on the remote machines (hontanon on caldera.example.com and ramon at redhat.example.com). This is just fine as long as you enter those keys correctly in `suse.example.com`'s .ssh/authorized_keys file.

# ### Using OpenSSH

The first time you start the sshd daemon, you'll see the following:

```
```text
[ramon]$ sudo /etc/rc.d/init.d/sshd start
Generating RSA keys:  Key generation complete.
Your identification has been saved in /etc/ssh/ssh_host_key.
Your public key has been saved in /etc/ssh/ssh_host_key.pub.
The key fingerprint is:
96:26:e0:4b:4e:9b:28:6d:e7:b9:92:65:lb:7a:7c:09 root@redhat.example. ¸com
Generating DSA parameter and key.
Your identification has been saved in /etc/ssh/ssh_host_dsa_key.
Your public key has been saved in /etc/ssh/ssh_host_dsa_key.pub.
The key fingerprint is:
09:92:6c:84:28:54:8b:45:7d:a7:d6:76:80:ld:2l:b2 root@redhat.example.com
Starting sshd: [ OK ]
```
```

As you can see, the daemon knows that it is running for the first time and it creates two sets of keys, both RSA and DSA for backward compatibility. These are the keys that the sshd daemon will use to authenticate itself to remote hosts from now on, similarly to the way you use RSA to authenticate at the user level.
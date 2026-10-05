# ssh_config Allowing many host files

| | 100% 1727 1.4M/s 00:00 |
| 05-redhat.conf | 100 690 1.6M/s 00:00 |
| ssh_config | 100 4469 9.5M/s 00:00 |
| ssh_host_ed25519_key | 100 387 1.2M/s 00:00 |
| ssh_host_ed25519_key.pub | 100 920 268.1K/s 00:00 |
| ssh_host_ecdsa_key | 100 492 1.5M/s 00:00 |
| ssh_host_ecdsa_key.pub | 100 162 537.7K/s 00:00 |
| ssh_host_rsa_key | 100 1799 4.9M/s 00:00 |
| ssh_host_rsa_key.pub | 100 382 1.2M/s 00:00 |

2.3 Verify that the /etc/ssh directory server is copied to the /home/serverbackup directory.

```
[student@servera ~]$ ls -LR ~/serverbackup
/home/student/serverbackup:
total 0
drwxr-xr-x. 3 student 245 Feb 11 18:35 ssh

/home/student/serverbackup/ssh:
total 588
-rw-r--r-- 1 student 563386 Feb 11 18:35 moduli
-rw-r--r-- 1 student 1727 Feb 11 18:35 ssh_config
-drwxr-xr-x. 2 student 28 Feb 11 18:35 ssh_config.d
-rw-r--r-- 1 student 4469 Feb 11 18:35 sshd_config
-rw-r--r-- 1 student 492 Feb 11 18:35 ssh_host_ecdsa_key
-rw-r--r-- 1 student 162 Feb 11 18:35 ssh_host_ecdsa_key.pub
-rw-r--r-- 1 student 387 Feb 11 18:35 ssh_host_ed25519_key
-rw-r--r-- 1 student 82 Feb 11 18:35 ssh_host_ed25519_key.pub
-rw-r--r-- 1 student 1799 Feb 11 18:35 ssh_host_rsa_key
-rw-r--r-- 1 student 382 Feb 11 18:35 ssh_host_rsa_key.pub

/home/student/serverbackup/ssh/ssh_config.d:
total 4
-rw-r--r-- 1 student student 690 Feb 11 18:35 05-redhat.conf
```

+   3. Exit from servera.

```
[student@servera -]$ exit
logout
Connection to servera closed.
[student@workstation]$
```

# Finish

On workstation, the lab archive-transfer finish script to complete this exercise.

```
[student@workstation -]$ lab archive-transfer finish
```

This concludes the guided exercise.
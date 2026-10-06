# Kemal Demirez | 255

```
root@porteus:~# ssh@192.168.43.2
root@192.168.43.2's password:
The programs included with the Kali GNU/Linux system are free software:
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/~/copyright.
Kali GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by= applicable law.
root@kemal:~# exit
csh
Connection to 192.168.43.2 closed.
root@porteus:~#
```

We can make ssh connection from Porteus to too.

```
root@kemal:~# ssh@porteus
The authenticity of host 'porteus (192.168.43.55)' can't be established.
EDSA key fingerprint is SHA256:ae83:53:bc:ca64:a8:fb42:25:a7:28:c5:96.
Are you sure you want to continue connecting (yes/no)?yes
Warning: Permanently added porteus.192.168.43.55 (ECDSA) to the list of known hosts.
root@porteus's password:
Last login: Fri Nov 27 21:42:49 2015
root@porteus:~# ls
Desktop/ Downloads/
root@porteus:~#
```

# Scp

Let's make an example with scp command which provides file-transfer in system using SSH. Let's transfer deneme file located under /root in Kali to Porteus. For this:

We should use scp /deneme root@192.168.43.5:/ command

```
root@kemal:~# ls Masaustu Resimler test VirtualBox VMs
deneme Genem Wizik Subtotlolar Videolar
deneme root@kemal:~# scp /deneme root@192.168.43.5:/nroot@192.168.43.5's password:
deneme                                100% 6 0.0KB/s 00:00
root@kemal:~#
```

Let's see if the file has been copied?

§
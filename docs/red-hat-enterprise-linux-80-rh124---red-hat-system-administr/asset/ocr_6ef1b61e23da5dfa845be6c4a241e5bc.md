# Chapter IV | Configuring secure ssh

```
[user01@host ~] ssh newest
The authenticity of your remotehost (172.25.20.12) can't be established.
ECDSA fingerprint is SHA256:aQS0PTOLrqCO2XGk0IYCa7apPKimerDoauk720.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added newest,172.25.250.12 (ECDSA) to the list of known
hosts.
user01@newhost: password:
...output omitted...
[user01@newhost ~$]
```

# SSH Known Hosts Key Management

If a server's key is changed the key was lost due to hard drive failure, replaced for some legitimate reason, you will need to edit the known hosts files to make sure the entry for the old public key is replaced with an entry of the new public key in order to log without errors.

Public keys are stored in the /etc/ssh/ssh_known_hosts and each users'/.ssh/known_hosts on the SSH client. Each public key is on one line. The first line is a list of hostnames and IP addresses that share public key. The second is the encryption algorithm used for the last key is the key itself.

```
[user01@host ~$] cat -/.ssh/known_hosts
remotehost,172.25.250.11 ecdsa-sha256-nistp256
AAAEYJZHHNLOYTTMIbbdhNYANTAAAMlDIhNYANTAAAABBOi0e+FlantG6jul8Ag5NJ
+R1ZI2bWe6Yur6+r1f0F0OEaGfZ1kM3VTfgXfH53DWhnIb+6zf8w==
```

Each SSH server must connect to its public key in the /etc/ssh directory files with the extension .pub.

```
[user01@remotehost ~$] ls -l /etc/ssh/*key.pub
/etc/ssh/ssh_host_ecdsa_key.pub /etc/ssh/ssh_host_ed25519_key.pub /etc/ssh/
_host_rsa_key.pub
```

> NOTE
it is a good practice to add entries matching a server's ssh_host_*.key.pub files to your ~/.ssh/known_hosts file or to the system-wide /etc/ssh/ssh_known_hosts file.

# REFERENCES

ssh(1), w(1), and hostname(1) man pages
For more information refer to the Using Secure Communications Between Two Systems With OpenSSH in the Red Hat Enterprise Linux 8.0 BETA Configuring and Managing Security Guide at
https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/configuring_and_managing_security/assembly-using-secure-communications-with-openssh-configuring-and-managing-security

314

RH12-RHEL8.0-en-1-202190507
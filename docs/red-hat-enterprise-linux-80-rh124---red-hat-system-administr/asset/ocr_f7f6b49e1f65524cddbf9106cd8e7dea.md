# INSTALLING AND UPDATING SOFTWARE PACKAGES

# PERFORMANCE CHECKLIST

In this lab, you will manage software repositories and module streams, and install and upgrade packages from those repositories and streams.

# OUTCOMES

You should be able to:

+   - Manage software repositories and module streams.

+   - Install and upgrade packages from repositories and streams.

+   - Install an RPM package.

# BEFORE YOU

Log in to workstation as student using student as the password.

On workstation, run the lab software-review start command. This script ensures that server1 is available. It also downloads any packages required for the lab exercise.

```
$student@workstation ~ lab software-review start
```

1. On server configure a software repository to obtain updates. The repository should be called /etc/yum.repos.d/errata.repo. It should access http://content.example/rhel18.0/x86_64/rhca-practice/errata. Do not check GPG signatures.

1.1. From workstation the ssh to log in to server as the student

```
$student@workstation ~$ ssh student@server1
Warning: Permanently added 'server1, 172.25.0.251' (ECDSA) to the list of known hosts.
Activate the web console: systemctl enable --now cockpit.socket
```

Last login: Thu Mar 7 15:17:22 2019

1.2. Use the su command to switch to the root user. The password is redhat.

```
$student@server1 ~$ su -
Password: redhat
[root@server1 #]
```
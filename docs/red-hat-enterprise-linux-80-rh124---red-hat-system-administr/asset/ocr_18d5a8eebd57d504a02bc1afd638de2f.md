+   5. Explore the status of the sshd service. This service is used for secure encrypted communication between systems.

+   5.1. Determine whether the sshd service is enabled to start at system boot.

```
[servera ~$]$ systemctl is-enabled sshd
enabled
```

+   5.2. Determine if the sshd service is active without displaying all of the status information.

```
[servera ~$]$ systemctl is-active sshd
active
```

+   5.3. Display the status of the sshd service.

```
[servera ~$]$ systemctl status sshd
* sshd.service - OpenSSH server daemon
   Loaded: loaded (/usr/lib/systemd/system/sshd.service; enabled; preset: enabled)
   Active: active (running since 2019-02-06 12:46:58 IST; 4h 21min ago)
   Docs: sshd(8)
      sshd.config(5)
   Main PID: 720 (sshd)
   Tasks: 1 (limit: 11406)
   Memory: 5.8M
   CGroup: /system.slice/sshd.service
      /usr/sbin/sshd -D -ciphers=aes256-gcm@openssh.com,sha256-poly1305@openssh.com,aes256-ctr,aes256-bc,aes128-gcm@openssh.com,aes128-ctr,aes128-bc -hmac=hmac-sha256-etm@openssh.com,hmac-sha256-sha
      gequi.init.example.com systemd[1]: Starting OpenSSH server daemon...
      server.la.example.com sshd[720]: Server listening on 0.0.0.0:port 22.
      server.la.example.com systemd[1]: Starting OpenSSH server daemon.
      server.la.example.com sshd[720]: Server listening on ::port 22.
      ...output_merged...
      server.la.example.com sshd[1380]: pam_unix(sshd:session): session opened for
      user by (uid=0)
```

Press Q to exit the command.

+   6. List the enabled or disabled services of all units service.

```
[servera ~$]$ systemctl list-unit-files --type=service
```

| UNIT FILE | STATE |
| arp-ethers.service | disabled |
| atd.service | enabled |
| audit.service | enabled |
| auth-rcpgss-module.service | static |
| autovt.service | enabled |
| blk-availability.service | disabled |
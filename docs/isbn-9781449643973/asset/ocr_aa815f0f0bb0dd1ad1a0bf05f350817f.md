```
```
[student@TargetFedora01 ~]$ sestatus
SELinux status:    enabled
SELinuxfs mount:   /selinux
Current mode:      enforcing
Mode from config file: permissive
Policy version:    24
Policy from config file: targeted
```
```

![](bbox=[0.34, 0.22, 0.68, 0.24])

+   28. The computer's current status is *enforcing*, but upon reboot, it will read from the configuration file and change over to *permissive* mode.

# Enable the Internal Host-Based IP Stateful Firewall

+   29. Enable firewall to start when entering runlevels 2 - 5. Type the command: `su -c 'chkconfig -level 2345 iptables on'` and press <enter>.
+   30. Password: ISS316Security
+   31. Start the firewall. Type the command: `su -c 'service iptables start'`
+   32. Password: ISS316Security

```
```
[student@TargetFedora01 ~]$ su -c 'chkconfig --level 2345 iptables on'
Password:
[student@TargetFedora01 ~]$ su -c 'service iptables start'
Password:      -
```
```

![](bbox=[0.36, 0.64, 0.67, 0.66])

+   33. Verify firewall is configure to start in runlevels 2 - 5. Type the command: `chkconfig iptables --list` and press <enter>.

```
```
[student@TargetFedora01 ~]$ chkconfig iptables --list
iptables       0:off     1:off     2:on      3:on      4:on      5:on      6:off
```
```

![](bbox=[0.37, 0.82, 0.66, 0.84])

# Provide Limited Sudo Access as Alternative to Logging in as Root User
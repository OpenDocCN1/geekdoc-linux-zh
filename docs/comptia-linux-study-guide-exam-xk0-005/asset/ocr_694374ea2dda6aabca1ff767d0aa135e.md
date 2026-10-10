# TABLE 6.12 Commonly used chkconfig utility formats

| Command | Description |
| --- | --- |
| *chkconfig service* | Check if the *service* is enabled at the current runlevel. If yes, the command returns a true (0). If no, the command returns a false (1). |
| *chkconfig service on* | Enable the *service* at the current runlevel. |
| *chkconfig service off* | Disable the *service* at the current runlevel. |
| *chkconfig --add service* | Enable this *service* at runlevels 0–6. |
| *chkconfig --del service* | Disable this *service* at runlevels 0–6. |
| *chkconfig --levels [levels] service on/off* | Enable (on) or Disable (off) this *service* at runlevels *levels*, where *levels* can be any number from 0 through 6. |
| *chkconfig --list service* | Display the runlevels and whether or not the *service* is enabled (on) or disabled (off) for each one. |

The first command in Table 6.12 can be a little confusing. Be aware that when the utility checks if the service is enabled at the current runlevel, a true or false is returned in the ? variable. Listing 6.26 shows an example of using this command and displaying the variable results.

# Listing 6.26 Using the chkconfig utility to check service status

```
```
# runlevel
3 5
#
# chkconfig --list sshd
sshd
0:off
1:off
2:on
3:on
4:on
5:on
6:off
#
# chkconfig sshd
# echo $?
0
#
# chkconfig --list ntpd
ntpd
0:off
1:off
2:off
3:off
4:off
5:off
6:off
#
```
```
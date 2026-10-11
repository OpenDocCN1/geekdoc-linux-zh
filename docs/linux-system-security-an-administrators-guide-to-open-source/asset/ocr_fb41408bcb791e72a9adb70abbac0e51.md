*Resources* on page 255 for more information about anonymous ftp servers) for internal use. Further suppose that your internal Security Policy requires all systems to run identd, but that it also specifies that internal access to ftp servers, like the one in the example above, is critical to productivity. To satisfy this criteria, you can implement TCP_wrappers to take different actions based on whether a given user is identifiable; you can also, as we see in Example 10-19, invoke different daemons based on the availability of a particular user identity. As indicated in Table 10.5 on page 206, tcpd will report KNOWN if a user's identity is known and UNKNOWN if it is not. Notice the use of @KNOWN in both in.ftpd rules in Example 10-19. Recall from Table 10.5 on page 206 that, in the case of client lists, this will match only if both the hostname and IP address are known. Therefore, a result of UNKNOWN for a hostname may mean that hostname resolution services are not working properly. The presence of this option forces a reverse lookup (regardless of compile-time options; see *Building TCP_Wrappers* on page 196). Further, in Example 10-19 we see entries in an /etc/hosts.allow file that distinguish between known and unknown users in the following way. By virtue of the fact that the entry *KNOWN@UNKNOWN* appears, whenever an incoming ftp request occurs tcpd will generate an RFC931 call (regardless of compile-time options) to get the incoming username. If it is successful, then the rule matches and in.ftpd -a -1 is invoked from the compile-time daemon source directory (*/usr/sbin* in the case of Red Hat 5.2/6.0). Note that the -1 flag to in.ftpd causes in.ftpd to log the connection, and the -a flag causes in.ftpd to check the /etc/ftpcaccess file. See the references cited in *Internet Services Resources* on page 255 and the ftpd(8) man page for more information.

# Example 10-19  Sample /etc/hosts.allow Using twist

```
```
# hosts.allow

KNOWN@UNKNOWN

in.ftpd: UNKNOWN@KNOWN: banners \
	/bin/echo "Policy Violation!" \
	| /bin/mail -s "$(h isn't running ident)" root@$(h),root@$(h); \
	twist PATH=/usr/sbin/extra/exec in.ftpd -1 -o -1

in.ftpd: PARANOID: banners /etc/security/banners/paranoid:
	spawn (/bin/echo "$(h reported being %$(h connected using '$)" | \
	/bin/mail -s "Alert! Hostname Lookup Failure!" root@&h)&deny

in.ftpd: ALL: deny
```
```

On the other hand, if the request to the client for the username fails, the username will resolve to UNKNOWN. In such a case, the connection is still allowed, but a special banner is displayed (presumably notifying the user that identd is not running on the client), and e-mail is sent to both root on the server (root@$(h)) and root on the client (root@$(h)) notifying the administrator that a Security Policy violation has occurred. Finally, we see the use of the *twist* option, which causes */usr/sbin/extra/exec in.ftpd -1 -o -1* to be invoked instead of */usr/sbin/in.ftpd -a -1*. The use of */usr/sbin/extra* (it is
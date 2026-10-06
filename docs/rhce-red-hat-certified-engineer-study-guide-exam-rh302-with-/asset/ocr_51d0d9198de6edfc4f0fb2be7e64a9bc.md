# Checking Service Status

To check the status of BIND, issue the command

```
/etc/rc.d/init.d/named status
```

# Forcing a Database Reload

You should instruct BIND to reload its database whenever you change a BIND configuration file. To instruct BIND to reload its database, issue the command

```
/etc/rc.d/init.d/named reload
```

# Logs

By default, BIND logs messages to the system log, /var/log/messages. If BIND is not functioning properly, check the log for error messages that point to the problem.

# Further Information

Extensive documentation on BIND is available in /usr/doc/bind-*. You can also find information on the Web, at the Internet Software Consortium’s Web site, www.isc.org.

Now take the time to complete Exercise 21.2, which gives you practical experience in configuring BIND.

EXERCISE 21.2
Installing and Configuring BIND

Next to SENDMAIL, BIND is perhaps the most difficult of Unix services to configure. However, you need not be a BIND expert to pass the RHCE exam. Perform the following steps to gain experience working with BIND:

+   1. Install BIND.
2. Create a set of zone files for a hypothetical domain. Use IP addresses from a reserved block, such as 192.168.1.0-192.168.1.255.
3. Configure /etc/named.conf to refer to your zone files.
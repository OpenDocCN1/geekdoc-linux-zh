named is allowed only to read files in that directory and not write there. This makes sense, since that directory contains only BIND configuration files—the named program shouldn’t ever need to write there. The second line in the excerpt allows named to read and write to files or directories under /var/lib/bind/. This also makes sense because BIND might (among other things) store slave zone files here, and since those files are written to every time the zone changes, named needs permission to write there.

# Enforce and Complain Modes

You might have noticed that the aa-status output mentions two modes: enforce and complain modes. In enforce mode, AppArmor actively blocks any attempts by a program to violate its profile. In complain mode, AppArmor simply logs the attempt but allows it to happen. The aa-enforce and aa-complain programs allow you to change a profile to be in enforce or complain mode, respectively. So if my /usr/sbin/named program did need to write to a file in /etc/bind or some other directory that wasn’t allowed, I could either modify the AppArmor profile to allow it or I could set it to complain mode:

```
$ sudo aa-complain /usr/sbin/named
Setting /usr/sbin/named to complain mode
```

If later on I decided that I wanted the rule to be enforced again, I would use the aa-enforce command in the same way:

```
$ sudo aa-enforce /usr/sbin/named
Setting /usr/sbin/named to enforce mode
```

If I had decided to modify the default rule set at /etc/apparmor.d/usr.sbin.named, I would need to be sure to reload AppArmor so it would see the changes. You can run AppArmor’s init script and pass it the reload option to accomplish this:

```
$ sudo /etc/init.d/apparmor reload
```

Be careful when you modify AppArmor rules. When you first start to modify rules, you might want to set that particular rule into complain mode and then monitor /var/log/syslog for any violations. For instance, if
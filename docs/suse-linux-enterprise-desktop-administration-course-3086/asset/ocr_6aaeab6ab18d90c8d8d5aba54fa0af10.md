The following excerpt of /etc/syslog-ng/syslog-ng.conf shows some filters used in SUSE Linux Enterprise Desktop 10:

```
```
#
# Filter definitions
#
filter f_iptables  { facility(kern) and match("IN=") and match("OUT="); };
};
filter f_console    { level(warn) and facility(kern) and not
                      filter(f_iptables) or level(err) and not facility(authpriv);
};
filter f_newsnotice { level(notice) and facility(news); };
filter f_newsrcit   { level(crit) and facility(news); };
filter f_newserr    { level(err) and facility(news); };
filter f_news       { facility(news); };
...
filter f_messages   { not facility(news, mail)
                      and not filter(f_iptables); };
...
```
```

As you can see, facility and priority (level) can be used within filters. However, it is also possible to filter according to the content of a line being logged, as in the f_iptables filter above. Combining the expressions with

+   - and
+     or
+   - or
+     or
+   - and not

allows you to create very specific filters.

# **Destinations**

Destinations define where messages can be logged. The general syntax is as follows:

```
```
destination <identifier> {
 destination-driver(params);
 destination-driver(params); ... };
```
```

Possible destinations are files, fifos, sockets, ttys of certain users, programs, or other hosts. A sample from /etc/syslog-ng/syslog-ng.conf looks like this:

```
```
destination console  { file("/dev/tty10" group(tty) perm(0620)); };
destination messages { file("/var/log/messages"); };
```
```
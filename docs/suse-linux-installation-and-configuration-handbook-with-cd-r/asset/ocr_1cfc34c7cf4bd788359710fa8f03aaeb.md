# Troubleshooting

*When I attempt to connect to the proxy server, I get an access denied message.*

The most common reason behind such a message is that the access rules are denying your access to the server or to the request that you made. Check your ACLs and http_access rules.

*I am having problems connecting to Hotmail from the proxy server; I get the error Intrusion Logged, Access Denied.*

This is because Hotmail requires that all connections be made from the same IP. To fix that, add the line

```
hierarchy_stoplist hotmail.com
```

to your squid.conf file.

*I get an error message saying Too many files open.*

This probably means that you are running out of file descriptors. To open a file, you need a file descriptor, and if you run out of them, you can't open new files. You can fix this by increasing the number of file descriptors on your system by typing the following command:

```
# echo 4024 > /proc/sys/fs/file-max
```

*I want to ban a long list of sites, but putting them all on the same ACL statement is a pain. Any ideas?*

Yes, just put them all in a file, with each on a line of its own. Then pass the name of the file to the ACL.
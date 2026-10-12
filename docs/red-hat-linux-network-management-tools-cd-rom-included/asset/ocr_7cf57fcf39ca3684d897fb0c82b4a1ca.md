Conversely, the opposite list can be displayed with the `-u` option. In this case, the hosts that don't respond are displayed:

```
# ping -u vermeer monet rodin louvre
vermeer
```

We can go a step further and place a list of targets inside a file for processing. Let's assume a file called `host-list` contains the following IP addresses:

```
10.0.2.75
10.0.2.100
10.0.2.150
10.0.2.151
10.0.2.152
10.0.2.153
10.0.2.200
10.0.2.201
```

By redirecting the input to the `host-list` file, **fping** can process a larger number of targets instead of requiring you to specify them one by one on the command line:

```
# fping < host-list
10.0.2.75 is alive
10.0.2.100 is alive
10.0.2.150 is alive
10.0.2.151 is alive
10.0.2.152 is alive
10.0.2.153 is alive
10.0.2.200 is alive
10.0.2.201 is alive
```

This is a more reasonable way to handle a large number of hosts.

If you prefer, the `-f` option can also be used instead of the file redirection above. Thus the commands

```
# fping < host-list
# fping -f host-list
```

are functionally equivalent and yield the same result. However, the `-f` option is restricted to the **root** user, while any system user can use the redirection option shown in the first example.

The `alive` and `not alive` options (`-u` and `-a`) are very handy and can be used in a variety of situations. For example, let's assume you want to be notified via Email when certain systems are down. A
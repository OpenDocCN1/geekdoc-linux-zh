```
httpd {
    host.hostname="httpd.mwl.io";
    tp4.addr="203.0.113.222";
    path="/jail/httpd";
}
```

Over dozens of jails, it saves a lot of trouble.

You can override the defaults within a jail's definition. If I don't want to mount devfs(5) in a jail, I would set mount.nODEVfs for that specific jail.

# ### jail.conf Variables

You can use variable substitutions in jails. While you can define some of these variables, you can also pull some from the jail's settings. Variables are expanded in double quotes and in unquoted strings, but not in single-quoted strings.

Here, I define a variable for the directory that contains all of my jails and use that inside my jail definition:

```
$j="/jail";
mariadb {
    path="$j/mariadb";
    --snip--
}
```

If I must move my jails to a new filesystem or pool, I can update jail.conf by changing the one variable rather than editing every definition.

# ### Parameters as Variables

Once you define a jail parameter, you can use it as a variable. Every jail has at least one parameter, name. You can use these parameters to further expand default settings.

```
$j="/jail";
path="$j/$name";
host.hostname="$name.mwl.io";

mariadb {
    tp4.addr="203.0.113.221";
}
```
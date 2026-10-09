
# Task 2:

Now let's create a group and add ourselves to it:

```bash
sudo groupadd foo

sudo usermod -a -G foo $USER
```

Verify that your user was added with: `grep ^foo /etc/group`

# Task 3:

You can use `groupmod` to change properties of the group, like its name:

```bash
sudo groupmod -n bar foo

grep ^bar /etc/group
```

Finally, clean up with `sudo groupdel bar`

# Notes:

Several directives in `/etc/login.defs` will affect the behavior of `groupadd` and `groupmod`. See the man pages for `groupadd`, `groupmod`, and `login.defs` for more information.

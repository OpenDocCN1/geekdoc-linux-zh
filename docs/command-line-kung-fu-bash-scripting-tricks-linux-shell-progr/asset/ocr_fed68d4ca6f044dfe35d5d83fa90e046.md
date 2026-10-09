$ DIRECTORY=$(echo $ENVIRONMENT | tr [:upper:][:lower:])

$ echo $ENVIRONMENT | sudo tee -a /etc/motd

$ tail -1 /etc/motd

PRODUCTION

$ sudo mkdir /var/www/$DIRECTORY

$ sudo tar zxf wwwfiles.tgz -C /var/www/$DIRECTORY

# Display Your Command Search Path in a Human Readable Format

```
$ echo $PATH | tr ':' '\n'
```

Reading a colon separated list of items isn't as easy for us humans as it is for computers. To substitute new lines for colons, use the `tr` command.

```
$ echo $PATH

/usr/bin:/bin:/usr/local/bin:/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/sbin

$ echo $PATH | tr ':' '\n'

/usr/bin
/bin
/usr/local/bin
/bin
/usr/bin
/usr/local/sbin
/usr/sbin
/sbin
```

# Create a Text File from the Command Line without
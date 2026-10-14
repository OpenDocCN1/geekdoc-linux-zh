The apache2 section at the end is also shorthand. By default Heartbeat will run the service with the start argument when a node becomes active and with the stop argument when a node is disabled. If you created a special script in /etc/ha.d/resource.d/ or /etc/init.d/ and wanted to pass special arguments, you would just list the service name, two colons, then the argument. For instance, if I created a special script called pageme that sent an SMS to a phone number, my haresources line might read

```
node1 172.16.245.222 apache2 pageme::650-555-1212
```

Once you have created your haresources file, copy it to /etc/ha.d/ on both nodes, and make sure that it stays identical.

# AUTHKEYS

The final step in the process is the creation of the /etc/ha.d/authkeys file. This file contains some method Heartbeat can use to authenticate a node with the rest of the cluster. The configuration file contains one line starting with auth, then a number that defines which line below it to use. The next line begins with a number and then a type of authentication method. If you use a secure private network like a crossover cable, your authkeys might just look like this:

```
auth 1
1 crc
```

This option doesn't require heavy CPU resources because the communications aren't signed with any particular key. If you are going to communicate over an open network, you will likely want to use either MD5 or SHA1 keys. In either case the syntax is similar:

```
auth 2
1 crc
2 sha1 thisisasecretshalkey
3 md5 thisisasecretmd5key
```

Here you can see I have defined all three potential options. The secret key you pass after sha1 or md5 is basically any secret you want to make up. Notice in the example above I set auth 2 at the top line so it will choose to authenticate with SHA1. If I had wanted to use MD5 in this example, I would set auth to 3 since the MD5 configuration is on the line that begins
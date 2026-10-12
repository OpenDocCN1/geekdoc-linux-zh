The default `/etc/ftpd`access file contains a class definition called `all`, which specifies that users of type `real`, `guest`, and `anonymous` can access the FTP server from anywhere. The wildcard `*` is used to denote "anywhere."

In the following example, FTP access is granted only to real users who access the server from the `206.171.50.0` network:

```
class    all    real 206.171.50.*
```

You can also use domain names instead of IP addresses, as in the following example:

```
class    all    real *.nitec.com *.ad-engine.com
```

The preceding class definition allows real users to log in from any machine in the `nitec.com` and `ad-engine.com` domains.

If you don't plan to allow anonymous or guest accounts on your FTP server, you can remove the `guest` and `anonymous` keywords from the default `type`list for the `all` class.

# deny

Syntax: `deny addr_glob message_file`

Default: none

This keyword is used to deny FTP service to hosts that match the IP addresses or domain names specified. For example,

```
deny  *.edu
```

tells the FTP server to deny access to anyone trying to access the server from a U.S. university. Here is another example:

```
deny  *.com   /etc/goaway.msg
```

This configuration denies FTP access to anyone in a `*.com` domain and also displays the `/etc/goaway.msg` file.

# limit

Syntax: `limit class n times message_file`

Default: none
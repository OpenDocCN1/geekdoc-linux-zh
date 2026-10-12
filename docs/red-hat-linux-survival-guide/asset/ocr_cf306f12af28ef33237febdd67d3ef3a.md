# who

Syntax: who

This command displays information about the users who are currently logged into a system. You can also use the w command for the same purpose.

# whoami

Syntax: whoami

This command displays your current username.

# User Commands for Accessing Network Services

The commands that I discuss in this section allow you to access various network services. You can use these tools to get finger information on a user, transfer files, browse Web pages, read and send e-mails, Telnet to other systems, and so on.

# finger

Syntax: finger user@host

This program allows you to query a finger daemon at the named host. For example, the following command requests a finger connection to the finger daemon running on the blackhole.integrationlogic.com server:

```
finger kabir@blackhole.integrationlogic.com
```

If the named host does not allow finger connections, this attempt fails. On success, the finger request displays information about the named user. If the user has a .plan file in the home directory, most traditional finger daemons display this file. Because finger has been used by hackers to cause security problems, most system administrators disable finger service outside their domains.
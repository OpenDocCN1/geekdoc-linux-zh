Each rule is on a separate line and is made up of three parts separated by colons: a daemon name, a client list, and a list of options. Here's a sample rule:

```
```ftpd : all : deny```
```

The daemon name is **ftpd**; the client list is **all**, meaning all hosts; and the option is **deny**, telling wrappers to reject all connections. Nobody can connect to the FTP server on this host unless an earlier rule explicitly grants access.

In the early examples, I refer to only two options: **accept** and **deny**. They allow and reject connections, respectively. We'll discuss the additional options later.

# ### Daemon Name

The daemon name is the program's name as it appears on the command line. For example, **inetd(8)** starts the **ftpd(8)** program when it receives an incoming FTP request. The Apache web server starts a program called *httpd*, so if your version of Apache supports wrappers, give the daemon name as **httpd**. (Note that Apache doesn't run out of **inetd**, but it can support wrappers anyway.) One special daemon name, **ALL**, matches all daemons that support wrappers.

If your system has multiple IP addresses, you can specify, as part of the daemon name, different wrapper rules for each IP address that a daemon listens on:

```
```ftpd@203.0.113.1 : ALL : deny
ftpd@203.0.113.2 : ALL : accept```
```

In this example, we have two daemon names, **ftpd@203.0.113.1** and **ftpd@203.0.113.2**. Each has a separate TCP wrapper rule.

# ### The Client List

The client list is a list of specific IP addresses, network address blocks, hostnames, domain names, and keywords, separated by spaces. Hostnames and IP addresses are simple: just list them.
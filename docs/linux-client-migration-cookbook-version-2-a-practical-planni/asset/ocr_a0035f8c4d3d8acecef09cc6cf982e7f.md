administrator to analyze and fix problems remotely (except networking problems that prevent remote access). It also enables the administrator to remotely run scripts to monitor clients and gain data about the state of the clients.

Monitoring of the clients is used to proactively prevent problems instead of reacting to users not able to work. It is used to detect problems with disks, memory, and CPU usage, or even with certain applications. There are several products and solutions available to monitor systems, from commercial products such as IBM Tivoli Software for OSS solutions as Nagios and Big Brother.

# 4.5.4 Rollout of additional or replacement clients

In a steady state situation (that is, after the initial rollout of Linux clients), there will still be requirements for on-going replacement and addition of client systems. For both tasks, there should always be an up-to-date system image that can be used to build the client. Some extra updates after installing the initial client should not be a problem, but building a new client should mean applying many updates after the initial image installation to bring it fully-to-date with the current supported image.

When replacing a client, there are several things that have to be taken into account:

+   * In the case of a thick client, personalization data has to be transferred from the old replaced client or restored from backup

+   * Configuration files need to be copied over.

+   * Care has to be taken that the old name for the system will not lead to extra unnecessary problems.

+   * When using a new name on a replacement, make sure that the old name is removed from server-side configurations.

> **Important:** In the case where windbind is used, take care to copy the windbind idmap file from the replaced client. Because this keeps track of domain user to uid and gid matching, this is very important for file ownership.

On Hat Enterprise Linux systems the windbind idmap file is:

```
/var/cache/samba/winbind_idmap.tdb
```

On Novell Linux Desktop and SUSE Linux systems the windbind idmap file is:

```
/var/lib/samba/winbind_idmap.tdb
```
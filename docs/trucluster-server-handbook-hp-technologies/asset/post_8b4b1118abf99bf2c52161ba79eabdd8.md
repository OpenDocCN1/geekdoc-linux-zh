
```text
# mknod /dev/volconfig c 41 0
# mknod /dev/voltrace c 41 1
# mknod /dev/voliod c 41 2
# mknod /dev/volinfo c 41 3
# checkrc
```

These additional steps are necessary when using LSM because “dn_setup –init” completely deletes the /devices directory as well as the contents of /dev, and dn_setup does not know about LSM. We’ll cover LSM in greater detail in Chapter 14.

## 7.5.2.2 How Can I Check My Device Special Files and Directory Hierarchy for Inconsistencies?

```text
# dn_setup --sanity_check
        Passed
```

Note that this is effectively the same as running “dsfmgr –zx”, although the “–z” switch is undocumented.

## 7.5.2.3 How Can I Create a Tape Device Special File from the Installation CD?

```text
# dn_setup -install_tape
```

As of this writing, there is no reference page for the dn_setup command. However, it is documented in the Tru64 UNIX System Administration manual prior to version 5.1B and the Tru64 UNIX Hardware Management manual as of version 5.1B.

## 7.6 References

- *Tru64* UNIX System Administration – versions 5.1, 5.1A, and 5.1B.
- *Tru64* UNIX Hardware Management – version 5.1B.
- Reference pages (noted within the text).

## Tru64 UNIX Cluster Hooks:

Event Manager

The Event Manager (EVM) is a new component added to Tru64 UNIX in the version 5.0 release of the operating system in response to customer requests to have common access to all system (and cluster) event information.

In previous releases, events that occurred on the system would likely be logged to one of two main loggers: the System Message Logger (syslogd) and the Binary Error Logger (binlogd) — although other logging methods could also be used. EVM works in cooperation with these other event loggers to consolidate information. Figure 8-1 illustrates the event path to EVM.

![](img/a0df85c2e542a8d6c913113908553aa4_194_0.png)

![](img/a0df85c2e542a8d6c913113908553aa4_196_0.png)

Figure 8-2: EVM root directory hierarchy

![](img/a0df85c2e542a8d6c913113908553aa4_196_1.png)

Figure 8-3: EVM /usr directory hierarchy

![](img/a0df85c2e542a8d6c913113908553aa4_197_0.png)

Figure 8-4: EVM /var directory hierarchy

## 8.2.1 EVM Resident Components

EVM has three primary components for event management:

- evmd
- evmchmgr
- evmlogger

### 8.2.1.1 The EVM Daemon (evmd)

The EVM daemon is the main distribution hub for EVM. It is started during system initialization at runlevel 2, although it cannot access remote connections until runlevel 3. Communication to evmd is handled via socket connections. Posting and subscription requests are handled directly by evmd.

However, event retrieval is handled by forking an event_get service program (actually, /usr/sbin/evmget_srv. See /etc/evmdaemon.conf).

The EVM daemon starts both the Channel Manager and the Logger processes as defined in the /etc/evmdaemon.conf file. In fact, it can be configured to start any site-defined synchronizing client process as well.

For more information, see the evmd(8) and the evmdaemon.conf(4) reference pages.

### 8.2.1.2 The EVM Channel Manager (evmchmgr)

The channel manager is responsible for the monitoring and cleanup of channels defined in the /etc/evmchannel.conf file, provided they have a monitor (fn_monitor) or cleanup (/fn_cleanup) service routine defined. The channel manager is started automatically by the evmd daemon and should not be run as a standalone program.

By default, evmchmgr will write any error output to stderr.

For additional information, see the evmchmgr(8) and the evmchannel.conf(4) reference pages.

### 8.2.1.3 The EVM Logger (evmlogger)

The logger program is a subscriber of EVM events as defined in the /etc/evmlogger.conf file. This daemon subscribes to events and then writes them to an eventlog (such as /var/adm/evmlog/evmlog.dated) or forwards them using a forward command (such as sending email to the root account). The logger is started automatically by the evmd daemon but can be run as a standalone program by creating a configuration file and starting an evmlogger process with the "-c" switch. For example:

```
# evmlogger -c $HOME/evm/myEVMLogger.conf
```

By default, the evmlogger will write any error output to stderr.

For additional information, see the evmlogger(8) and the evmlogger.conf(4) reference pages.

# The Solaris Service Management Facility

# 3.6 BOOTING SOLARIS

With the introduction of its Service Management Facility, Sun revamped the boot process for Solaris 10 and OpenSolaris. SMF is a comprehensive and conceptually unique approach to managing services under UNIX. It wraps a new layer of logic around services to handle dependencies and automatically manage configuration errors and software failures.

SMF changes the boot process quite a bit. The traditional tableau of init and its rc scripts are, in theory, gone. Sun claims that modern applications and their dependencies have become too complex for the standard scheme. They're kind of right. On the other hand, the standard architecture is much simpler, and we-facetiously wonder how Linux and other popular operating systems could possibly be managing to limp along under the old system.

Before deciding the boot process, we need to take a general look at SMF.

# The Solaris Service Management Facility

Sun defines a service as "an entity that provides a list of capabilities to applications and other services, local and remote." For our purposes, a service is roughly equivalent to a daemon: a web server, the syslog system logger, or even init. Multiple instances of the same SMF service exist. For example, you might run several email servers with different configurations and IP addresses. A service can also be defined as a collection of other services. This feature lets SMF subsum the role of init's traditional rules.

Each instance of a service is uniquely identified by a "fault management resource identifier" or FMRI. For example, the following FMRIs refer to the SSH service:

```
svc/network/ssh:default
network/ssh:default
```

The ssh service is in the network category, and this FMRI describes the default instance. SMF includes several categories, such as application, device, network, and system. A special category called milestone encapsulates the count of run levels.

You examine the status of services with the svcs commands. Use svcs -a to see all services that have been defined, or omit the -a flag to see only those that are currently running. svcs can also examine an individual service. For example, the following command reveal the status of the SSH service:

```
solaris$ svcs -l svc:/network/ssh:default
fmri
svc/network/ssh:default
SSH server
enabled
true
state
line
next_state
none
state_time
Mon Jul 13 15:56:19 2009
```

![](bbox=[0.95, 0.191, 0.995, 0.275])
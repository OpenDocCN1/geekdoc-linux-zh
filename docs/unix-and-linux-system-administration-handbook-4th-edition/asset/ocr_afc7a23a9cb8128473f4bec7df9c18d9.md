The refuse action is more conformant to the DNS specification than deny because clients assume that unanswered queries were lost on the network rather than having been administratively dropped for policy reasons. The allow action is the one to use for normal DNS clients.

allow-snoop answers iterative queries as well as recursive queries. You can use it to investigate the contents of the server’s cache, since an iterative query succeeds only if the answer is already in-cache. allow-snoop can also be exploited for unwholesome purposes, so limit this action to your sysadmins’ hosts.

Security

| chroot: directory | [/usr/local/etc/unbound] |
| username: name | [unprivileged] |

The username option specifies the unprivileged user as whom unbound should run once it has completed its startup housekeeping.

The chroot directive tells unbound to run in a chrooted jail. You will have to jump through some hoops to make sure that everything unbound needs is available from the jail directory, but recent versions of the code make this pretty easy.

The code is smart about mapping global pathnames into the chrooted world. Most paths can be specified as absolute global paths, as absolute paths within the jail directory, or as paths relative to the working directory. unbound performs the appropriate mapping when necessary.

A couple of fine points about running unbound in jail: Reading the config file of course predates the chroot, so the config file specified on unbound’s command line should be a global path. The PID file, the unbound-control key files, and the syslog socket can all remain outside the jail directory because they are opened before unbound performs its chroot.

unbound reads /dev/random before chrooting, but it’s still a good idea to make /dev/random available after the chroot. unbound may need to return to it later to obtain more random data. If unbound cannot reach /dev/random, it uses a default source of randomness and logs a warning message.

![](bbox=[0.22, 0.00116, 0.28, 0.00128])

Under Linux, you can make /dev/random available in the jail with the following incantation (which assumes that /var/unbound is your jail directory):

```
linux$ sudo mount --bind -n /dev/random /var/unbound/dev/random
```

ID variables

The following options control whether unbound tells the truth about its version and hostname when queried for the CHAOS names id.server and version.server:

| hide-identity: yes | no |
| identity: string | [hostname] |
| hide-version: yes | no |
| version: string | [name server version] |

As explained on page 598, we recommend not tampering with these values.
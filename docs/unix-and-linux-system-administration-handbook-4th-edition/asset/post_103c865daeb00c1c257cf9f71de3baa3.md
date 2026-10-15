
# Locations

directory: directory [/usr/local/etc/unbound]
pidfile: filename [/usr/local/etc/unbound/unbound.pid]
root-hints: filename [none]

The directory option sets the server’s working directory. unbound defaults to a directory under /usr/local/etc, but many sites prefer /var. The location of the PID file defaults to unbound’s working directory, but it also works fine in more traditional places such as /var/run.

Root hints are built into unbound’s code, so the hints file is not required. However, you can provide one if you like since the addresses in the code may eventually become out of date. Use dig . ns to obtain a fresh copy occasionally, or if you are really paranoid, try dig @a.root-servers.net . ns for an authoritative copy.

## Logging

use-syslog: yes | no [yes]
logfile: filename [none]
log-time-ascii: yes | no [no]
verbosity: level [1]

Logging information can go either to syslog or to a file. Choose between them with the use-syslog and logfile options. If you want normal time instead of UNIX time (seconds since 1/1/1970) in log messages, turn on the log-time-ascii option. The verbosity determines the amount of logging; see page 673 for details.

## Statistics

statistics-interval: seconds [0, i.e., disabled]
statistics-cumulative: yes | no [no]
extended-statistics: yes | no [no]

Statistics are turned off by default because they slow down the name server. If you turn them on by setting the statistics-interval option to a nonzero number of seconds, statistics will be written to the log file (or to syslog) at the specified interval. By default, the statistics counters are reset to 0 each time they are written out; use the statistics-cumulative option to make them accumulate over time.

Setting extended-statistics to yes generates more data that you can dump using unbound-control.

See page 886 for more information about Cacti and RRDtool.

The distribution’s contrib directory contains plug-ins that connect Cacti or Munin to the running name server and that graph real-time statistics with RRDTool. See the statistics how-to at unbound.net for details.

## Query access

access-control: netblock action [allow only localhost]

The access-control option is the key to configuring unbound to be a recursive name server for your own users and not for the rest of the world. Use multiple access-control lines to allow multiple networks. The action parameter can take on four values:

- deny – blocks all queries from the specified network or host
- refuse – blocks queries and sends a REFUSED message back
- allow – answers queries from clients requesting recursion
- allow-snoop – answers queries from recursive and iterative clients

The refuse action is more conformant to the DNS specification than deny because clients assume that unanswered queries were lost on the network rather than having been administratively dropped for policy reasons. The allow action is the one to use for normal DNS clients.

allow-snoop answers iterative queries as well as recursive queries. You can use it to investigate the contents of the server’s cache, since an iterative query succeeds only if the answer is already in-cache. allow-snoop can also be exploited for unwholesome purposes, so limit this action to your sysadmins’ hosts.

## Security

| chroot: directory | [/usr/local/etc/unbound] |
| username: name | [unprivileged] |

The username option specifies the unprivileged user as whom unbound should run once it has completed its startup housekeeping.

The chroot directive tells unbound to run in a chrooted jail. You will have to jump through some hoops to make sure that everything unbound needs is available from the jail directory, but recent versions of the code make this pretty easy.

The code is smart about mapping global pathnames into the chrooted world. Most paths can be specified as absolute global paths, as absolute paths within the jail directory, or as paths relative to the working directory. unbound performs the appropriate mapping when necessary.

A couple of fine points about running unbound in jail: Reading the config file of course predates the chroot, so the config file specified on unbound’s command line should be a global path. The PID file, the unbound-control key files, and the syslog socket can all remain outside the jail directory because they are opened before unbound performs its chroot.

unbound reads /dev/random before chrooting, but it’s still a good idea to make /dev/random available after the chroot. unbound may need to return to it later to obtain more random data. If unbound cannot reach /dev/random, it uses a default source of randomness and logs a warning message.

![](img/14d78e3cecac4581d37024baf1e94cca_683_0.png)

Under Linux, you can make /dev/random available in the jail with the following incantation (which assumes that /var/unbound is your jail directory):

```
linux$ sudo mount --bind -n /dev/random /var/unbound/dev/random
```

## ID variables

The following options control whether unbound tells the truth about its version and hostname when queried for the CHAOS names id.server and version.server:

| hide-identity: yes | no |
| identity: string | [hostname] |
| hide-version: yes | no |
| version: string | [name server version] |

As explained on page 598, we recommend not tampering with these values.

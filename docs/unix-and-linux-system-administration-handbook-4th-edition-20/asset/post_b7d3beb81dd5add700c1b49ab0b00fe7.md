
# Using unbound-control

# Table 17.16 rndc commandsᵃ

| Command | Function |
|---|---|
| dumpdb | Dumps the DNS database to named_dump.db |
| flush [view] | Flushes caches or those for a specified view |
| flushname [view] | Flushes the specified name from the server's cache |
| freeze zone [class] | Suspends updates to a dynamic zone |
| thaw zone [class] | Resumes updates to a dynamic zone |
| halt | Halts named without writing pending updates |
| querylog | Toggles tracing of incoming queries |
| notify zone [class] | Resends notification messages for zone |
| notrace | Turns off debugging |
| reconfig | Reloads the config file and loads any new zones |
| recursing | Dumps queries currently recurring, named.cursing |
| refresh zone [class] | Schedules maintenance for a zone |
| reload | Reloads named.conf and zone files |
| reload zone [class] | Reloads only the specified zone or view |
| restart | Starts the server |
| transfer zone [class] | Recopies the data for zone from the master server |
| stats | Dumps statistics to named.stats |
| status | Displays the current status of the running |
| stop | Saves pending updates and stops named |
| trace | Increases the debug level by 1 |
| trace level | Changes the debug level to that value level |
| validation newState | Enables/disables DNSSEC validation on the fly |

a. The class argument here is as for resource records, typically IN for Internet.
b. Not implemented in BIND 9 (9.7.0), but it has been promised forever—must be hard to do.

# Using NSD's nscd

NSD's control program, nscd, is a shell script that uses signals to control the behavior of nsd and zonec, its precompiler companion. nscd must be running on the same machine as nsd, keys are not needed.

nscd has a smaller repertoire of commands than rndc, as shown in Table 17.17 on the next page. When run, nscd reads the nsd.conf configuration file and uses the nsd-check utility to verify that there are no syntax errors.

# Using unbound-control

unbound-control talks to the unbound name server through TLS, the transport layer security protocol (formerly known as SSL), which uses a key and a certificate for each end. These keys are configured in the remote-control section of the config unbound.conf. More than 20 commands can be given remotely to modify the server's behavior. Rather than list all possible commands, we refer to the an page for unbound-control, where they are well documented.

# Chapter 17 DNS: The Domain Name System

# Table 17.17 nsdc commands

| Command | Function |
|---|---|
| start | Starts the nsd server |
| stop | Stops the nsd server (ends SIGTERM) |
| reload | Reloads the compiled zone database |
| rebuild | Rebuilds the zone database with zonec |
| restart | Starts nsd; that is, it stops and then starts it |
| running | Checks whether nsd is running; no output means all's well |
| update | Tries to update all slave zones |
| notify | Sends messages to all slave servers |
| patch | Merges zone transfer changes (database) back to zone files (text) |

The 20 are the usual start, stop, and reread types, but also several options that allow fine-grained control of the cache and the local data zones that have been configured. Options such as forwarding can be configured or modified on the fly. You can dump or reload the cache as well.

# Name server statistics

Each of our name server collects statistics with varying granularity and can dump them to a file on request. Several options are configurable: what data to collect, where to write it, how often to update it, and so on. Our new statistics channel is the most flexible mechanism. NSD's attitude is that it's a sleek, speedy name server and if you want statistics, another program would gather them and let NSD get on with its primary job. unbound is somewhere in the middle.

BIND and unbound can both send their statistics to another program for presentation and graphing. BIND uses the new statistics-channels statement (page 612) and XML. unbound uses plug-ins in the contrib directory to connect to either M own or Cacti (see page 886).

named maintains summary information that can be dumped to named.stats in named's working directory on receipt of a nudge from rndc.

Here's a small snippet of the output from the server in vix.com domain. Lots has been left out; about 20 groups of data are shown, but we include two:

```
+++ Statistics Dump +++ (1248150900)
++ Incoming Queries ++
2650862 A
9105 NS
40438 SOA
85744 PTR
246258 MX
3208092 TXT
...
```

# Debugging with dig

```
++ Name Server Statistics ++
10028960 IPv4 requests received
388015 IPv6 requests received
5896039 requests with EDNS(0) received
92403 TCP requests received
436730 queries resulted in successful answer
761430 queries resulted in successful answer

# Debugging with dig

# Lame delegations

The effects of a lame delegation can be very bad. If one of your servers is lame, your DNS system is less efficient. If all the name servers for a domain are lame, no one can reach you.

There are two ways to find lame delegations: by reviewing the log files and by using a tool, short for 'domain occupancy'. We look at doc examples in the next section, let's first review some log entries.

Many sites point the lame-servers logging to /dev/null and don't fretting about other people's lame delegations. That's fine as long as your own domain is sneaky and it is not a source or victim of lame delegations. The lame server serves DNS down; if all servers are lame, your domain is essentially off the air.

Here is a logging example. We have truncated the output to tame dig's verbosity; the +short flag dig limits the output even more.

```
Jul 19 14:37:50 nubark named[757]: lame server resolving 'w33.com' (in
w33.com?): 216.171.131.583
```

Digging for name servers for w33.com at one of the gTLD servers yields

```
$ dig @egtld-servers.net w33.com ns
;; ANSWER SECTION:
w33.com.      14400 IN ns ns0.nameserver.net.
w33.com.      14400 IN ns ns1.nameserver.net.
```

But if we ask each of these servers in turn that same question, will we get an answer from ns0 and no answer from ns1:

```
$ dig @ns0.nameserver.net w33.com ns
;; ANSWER SECTION:
w33.com.      14400 IN ns ns0.nameserver.net.
w33.com.      14400 IN ns ns1.nameserver.net.
```

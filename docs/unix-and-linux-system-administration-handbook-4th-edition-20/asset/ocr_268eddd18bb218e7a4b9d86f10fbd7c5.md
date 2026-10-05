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

+   a. The class argument here is as for resource records, typically IN for Internet.
b. Not implemented in BIND 9 (9.7.0), but it has been promised forever—must be hard to do.

# Using NSD's nscd

NSD's control program, nscd, is a shell script that uses signals to control the be-havior of nsd and zonec, its precompiler companion. nscd must be running on the same machine as nsd, keys are not needed.

nscd has a smaller repertoire of commands than rndc, as shown in Table 17.17 on
t next page. When run, nscd reads the nsd.conf configuration file and uses the
sd-check utility to verify that there are no syntax errors.

# Using unbound-control

unbound-control talks to the unbound name server through TLS, the transport
layer security protocol (formerly known as SSL), which uses a key and a certificate
for each end. These keys are configured in the remote-control section of the con-fig unbound.conf. More than 20 commands can be given remotely to modify
the server's behavior. Rather than list all possible commands, we refer to the
an page for unbound-control, where they are well documented.
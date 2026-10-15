unbound also has a -d flag to turn on debugging mode. You can boost the verbosity of the debugging information with the -v flag; for more, try -v -v. Debugging output is separate from the verbosity of logging information set in the config file. You can configure additional logging to help debug DNSSEC signature validation issues; see page 666.

# Name server control programs

All three of our name servers come with a control program: nsdc controls nsd, rndc controls named, and unbound-control controls unbound. nsdc works on the local machine only, but rndc and unbound-control can work across the Internet if you set them up that way.

rndc uses a network socket to communicate with named and uses TSIG authentication for security. unbound-control uses SSL/TLS, and nsdc uses signals.

Using BIND’s rndc

Table 17.16 shows some of the options accepted by rndc. Typing rndc with no arguments gives a list of available commands and a short description of what they do. Earlier incarnations of rndc used signals as nsdc does, but with over 25 commands, the BIND folks ran out of signals long ago. Commands that produce files put them in whatever directory is specified as named’s home in named.conf.

rndc reload makes named reread its configuration file and reload zone files. The reload zone command is handy when only one zone has changed and you don’t want to reload all the zones, especially on a busy server. You can also specify a class and view to reload only the selected view of the zone’s data.

Note that rndc reload is not sufficient to add a completely new zone; that requires named to read both the named.conf file and the new zone file. For new zones, use rndc reconfig, which rereads the config file and loads any new zones without disturbing existing zones.

rndc freeze zone stops dynamic updates and reconciles the journal of dynamic updates to the data files. After freezing the zone, you can edit the zone data by hand. As long as the zone is frozen, dynamic updates are refused. Once you’ve finished editing, use rndc thaw zone to start accepting dynamic updates again.
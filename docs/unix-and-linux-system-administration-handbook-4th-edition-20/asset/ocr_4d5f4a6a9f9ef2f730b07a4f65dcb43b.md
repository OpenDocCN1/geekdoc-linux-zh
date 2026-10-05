# Chapter 17 DNS: The Domain Name System

unbound also has a -d flag to turn on debugging mode. You can boost the verbosity of the debugging information with the -v flag; for more, try -v -v. Debugging output is separate from the verbosity of logging information set in the config file. You can configure additional logging to help DNSSEC signature validation issues; use page 666.

# Name server control programs

All of three our name servers come with a control program: nsd controls nsd, rndc controls named, and unbound-control controls unbound. nsd works on the local machine only, but rndc and unbound-control can work across the Internet if you set them up that.

rndc uses a network socket to communicate with named and TSIG authentication for security. unbound-control uses SSL/TLS, and nsd uses signals.

Using BIND's rndc

Table 17.16 shows the options accepted by rndc. Typing rndc with no arguments gives a list of available commands and a short description of what they do. Earlier instances of rndc used signals as nsd does, but with over 25 commands, BIND folks ran long ago. Commands put them in whatever directory is specified as named's home in named.conf.

rndc reload makes named read its configuration file and reload zone files. The reload command is handy when only one zone has changed and you don't want to reload all the zones, especially on a busy server. You can also specify a class and view to reload only the selected zone of the zone's data.

Note that rndc reload is not sufficient to add a completely new zone; that requires named to read both the named.conf and the new zone file. For new zones, use rndc reconfig, which reloads the config file and any new zones without disturbing existing zones.

rndc freeze stops dynamic updates and reconciles the journal of dynamic updates to the data files. After freezing the zone, you can edit the zone data by hand. As long as the zone is frozen, dynamic updates are refused. Once you've finished editing, use rndc thaw zone to start accepting dynamic updates.

rndc dumpdb makes named dump its database to named_dump.db. The dump file is big and includes not only local data but also cached data the name server has accumulated.

Your versions of named must match or you will get an error message about a protocol version mismatch. They're normally installed together on individual machines, but version skew can be an issue when you are trying to control named on another computer.
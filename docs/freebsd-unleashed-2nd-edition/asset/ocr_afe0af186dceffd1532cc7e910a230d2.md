# LISTING 31.1 Continued

```
zone " . " {
type hint;
file "named.boot";
};

zone "0.0.127.in-addr.arpa" {
type master;
file "localhost.rev";
};

zone "0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.IP6.INT" {
type master;
file "localhost.rev";
};
```

As shown in the listing, a configuration file consists of a number of blocks (or *statements*) in C-style syntax, with substatements allowed within curly brackets (`{}`) . All possible statements are listed and described in the *man named.conf* page. Some of the most useful ones are options, controls, logging, and zone.

Comments in *named.conf* are also C style; single-line comments are done with double slashes (`//`) , and block comments are done with the `/* comment */` syntax. Shell-style comments (`#`) are also supported.

The *named.conf* file that exists in the default installation of FreeBSD has a few of the statements shown in Listing 31.1 and a few that are not. It also has a lot of inline documentation that describes how to use each of them.

Whenever you make a change to *named.conf* or to any of the zone files (which we will discuss later in this chapter), restart *named* using the *ndc* program:

```
# ndc reload
Reload initiated.
```

# Using a Forwarder

Recalling the topology shown in Figure 31.1, a *forwarder* is a name server at an “upstream” network—a larger network “closer” to the root servers—that allows you to request DNS information from it. (Note that access to a name server can be restricted, as you will see.) A good candidate for a forwarder is your uplink ISP’s name server, if your FreeBSD machine is acting as a name server for a home network. Normally, if your machine can't answer a DNS request on its own, it must query the root servers (found in `/etc/namedb/named.root`) for the authoritative reply. These extra steps take time and add to the packet traffic on the network.
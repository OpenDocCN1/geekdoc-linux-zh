
# Chapter 6. BIND 9 Configuration Reference

Zones defined within a view statement will only be accessible to clients that match the view. By defining a zone of the same name in multiple views, different data can be given to different clients, for example, "internal" and "external" clients in a split DNS setup.

Many of the options in the options statement can also be used within a view statement, and then apply only when resolving queries with this view. When no view-specific value is given, the value in the options statement is used as a default. Also, zone options can be specified in the view statement; these view-specific defaults take precedence over those in the options statement.

Views are class specific. If no class is given, class IN is assumed. Note that all non-IN views must contain a hint zone, since only the IN class has compiled-in default hints.

If there are no view statements in the config file, a default view that matches any client is automatically created in any zone statements specified on the top level of the configuration file are considered to be part of this default view. If any explicit view statements are present, all zone statements must occur inside view statements.

Here is an example of a split DNS setup implemented using view statements.

```
view "internal" {
    // This should match our internal networks.
    match-clients { 10.0.0.0/8 };
    // Provide recursive service to internal clients only.
    recursion yes;
    // Provide a complete view of the example.com zone
    // including addresses of internal hosts.
    zone "example.com" {
        type master;
        file "example-internal.db";
    }
}
view "external" {
    match-clients { any };
    // Refuse recursive service to external clients.
    recursion no;
    // Provide a restricted view of the example.com zone
    // containing only publicly accessible hosts.
    zone "example.com" {
        type master;
        file "example-external.db";
    }
}
```

## 6.2.21. zone Statement Grammar

```
zone zone_name [class] {
  type ( master | slave | hint | stub | forward ) ;
  allow-notify { address_match_list } ;
  allow-query { address_match_list } ;
  allow-transfer { address_match_list } ;
  allow-update { address_match_list } ;
  update-policy { update_policy_rule [...] } ;
  allow-forwarding { address_match_list } ;
  also-notify { ip_addr [port_addr] ; [ ip_addr [port_addr] ... ] };
  check-names (fail|ignore) ;
  dialup dial_option ;
  file string ;
  forward (only first) ;
  forward-ers { ip_addr [port_addr] ; [ ip_addr [port_addr] ... ] };
  ifconfig-base string ;
  ifconfig-tmp-file string ;
  maintain-ifconfig yes_or_no ;
  masters [port_addr] ; [ ip_addr [port_addr]] ;
  max-ifconfig-log-size number ;
  max-transfer-idle number ;
  max-transfer-time number ;
  max-transfer-timeout number ;
  notify yes_or_no explicit ;
  pubkey number ;
  transfer-source { ip4addr | * } [port_addr] ;
  transfer-source-v6 { ip6addr | * } [port_addr] ;
  notify-source { ip4addr | * } [port_addr] ;
  notify-source-v6 { ip6addr | * } [port_addr] ;
  zone-statistics yes_or_no ;
  sig-valid-interval number ;
  database string ;
  min-refresh-time number ;
  max-refresh-time number ;
  min-retry-time number ;
  max-retry-time number ;
}
```

## 6.2.22. zone Statement Definition and Usage

### 6.2.22.1. Zone Types

| Type | Description |
| :--- | :--- |
| master | The server has a master copy of the data for the zone and will be able to provide authoritative answers for it. |
| slave | A slave zone is a replica of the master zone. The masters list specifies one or more IP addresses of master servers that the slave contacts to update its copy of the zone. By default, transfers are made from port 53 on the servers; this can be changed for all servers by specifying a port number before the list of IP addresses, or on a per-server basis. Authentication to the master can also be done with per-server TSIG keys. If a file is specified, then the replica will be written to this file whenever the zone is changed, and reloaded from this file on restart. Use of a file is recommended, since it often speeds up start-up and eliminates (in the tens or thousands of zones per server, it is best to use a two-level naming scheme for zone names. For example, a slave server for the zone example.com might place the zone contents into a file called ex/example.com where ex/ is just the first two letters of the zone.) |
| stub | A stub zone is similar to a slave zone, except that it replicates only the NS records of a master instead of the entire zone. This meant that in some cases, users could get away with configuring stubs only in the master server for the parent zone. BIND 9 never allows zone data from different zones in this way. Therefore, if BIND 9 mastering a parent zone has child zones configured, all the slave servers for the parent zone also need to have the same stub zones configured. Stub zones can also be used as a way of forcing the resolution of a given domain to use a particular set of authoritative servers. For example, the caching name servers on a private network using RFC2157 addressing may be configured with stub zones for 10.in-addr.arpa to use a set of internal name servers as the authoritative servers for that domain. |
| forward | "A forward" is a way to configure forward on a per-domain basis. A zone statement of type forward can contain a forward and/or forwarders statement, which will apply to queries within the domain given by the zone name. If no forwarders statement is present or an empty list for forwarders is given, no forwarding will be done for the domain, cancelling the effects of any forwarders in the options. Thus if you want to use this type of zone to change the behavior of the global forward option (that is, "forward first to", "forward only", or vice versa, but want to use the same servers as set globally) you need to specify the global forwarders. | Stub zones are not a standard part of the DNS; they are a feature specific to the BIND implementation. This usage is not recommended for new configurations, and BIND 9 supports it in a limited way. |

## 6.2.22.2. Class

The zone's name may optionally be followed by a class. If a class is not specified, class IN (for Internet), is assumed. This is correct for the vast majority of cases.

The hesiod class is named for an information service from MIT's Project Athena. It is used to share information about various systems databases, such as users, groups, printers and so on. The keyword HS is a synonym for hesiod.

Another MIT development is CHAOSnet, a LAN protocol created in the mid-1970s. Zone data for it can be specified with the CHAOS class.

## 6.2.22.3. Zone Options

- allow-notify: See the description of allow-notify in Section 6.2.14.3
- allow-query: See the description of allow-query in Section 6.2.14.3
- allow-transfer: See the description of allow-transfer in Section 6.2.14.3.
- allow-update: Specifies which hosts are allowed to submit Dynamic DNS updates for master zones. The default is to deny updates from all hosts.
- update-policy: Specifies a "Simple Secure Update" policy. See Section 6.2.22.4.

The initial set of root nameservers is specified using a "hint zone". When the server starts up, it uses the root hints to find a root nameserver and get the most recent list of rootervers. If no hint zone is specified for class IN, the server uses a compiled-in default of root servers hints. Classes other than IN have no built-in defaults.

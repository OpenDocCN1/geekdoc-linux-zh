```
# Use with the following in named.conf, adjusting the allow list as needed:
# key "rndc-key" {
#     algorithm hmac-md5;
#     secret "orZuz5amkUnEp52zIHxD6cd5hACl dOGsG/elP/dv2IY=";
# };
# controls {
#     inet 127.0.0.1 port 953
#     allow { 127.0.0.1; } keys { "rndc-key"; };
# };
# End of named.conf
```

# Split DNS and the view statement

Many sites want the internal view of their network to be different from the view seen from the Internet. For example, you might reveal all of a zone’s hosts to internal users but restrict the external view to a few well-known servers. Or, you might expose the same set of hosts in both views but supply additional (or different) records to internal users. For example, the MX records for mail routing might point to a single mail hub machine from outside the domain but point to individual workstations from the perspective of internal users.

> See page 462 for more information about private address spaces.

A split DNS configuration is especially useful for sites that use RFC1918 private IP addresses on their internal networks. For example, a query for the hostname associated with IP address 10.0.0.1 can never be answered by the global DNS system, but it is meaningful within the context of the local network. Of the queries arriving at the root name servers, 4%–5% are either from an IP address in one of the private address ranges or about one of these addresses. Neither can be answered; both are the result of misconfiguration, either of BIND’s split DNS or Microsoft’s “domains.”

The view statement packages up a couple access lists that control which clients see which, some options that apply to all the zones in the view, and finally, the zones themselves. The syntax is

```
view view-name {
    match-clients { address_match_list ; }    [any]
    match-destinations { address_match_list ; } [any]
    match-recursive-only yes | no;             [no]
    view_option;
    zone_statement; ...
};
```

Views have always had a match-clients clause that filters on the source IP address in the query packet and is typically used to serve internal and external views of a site’s DNS data. For finer control, you can now also filter on the query destination address and can require recursive queries. The match-destinations clause looks at the destination address in the query packet and is useful on multihomed machines when you want to serve different DNS data depending on the interface on
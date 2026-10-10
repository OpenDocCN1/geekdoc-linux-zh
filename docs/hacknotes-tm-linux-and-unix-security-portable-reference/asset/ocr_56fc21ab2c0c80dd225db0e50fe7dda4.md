# REGIONAL INTERNET REGISTRIES

Similar to domain names, organizations can be allocated blocks of IP ad-  
dresses. Routable IP addresses are allocated to organizations by four  
main Regional Internet Registries (RIRs), as shown in Table 1-1.

Table 1-1 contains a list of four major RIRs. However, some new RIRs are sched-  
uled to be established in the near future. See http://www.aso.icann.org/ for de-  
tails and updates.

Many registrars restrict the types of queries mentioned in the following sections. If  
any of the following queries do not result in a positive response from a particular  
whois server, they just might work against the whois server of another registrar.

# Querying RIR Records by Company Prefix

To find records owned by a company name, a whois query can be per-  
formed like this:

```
whois -h whois.rirwhoisserver.net "companynameprefix"
```

To search RIR records for company names beginning with the word  
“somecompanyasanexample”:

```
[bash]$ whois -h whois.rirwhoisserver.net "somecompanyasanexample"
Some Company (SOMEC)
Some Company As An Example (SOMECA)

# RIR Whois database, last updated on 2003-01-11 01:00
```

| Name | Whois Server | Region |
| :--- | :--- | :--- |
| American Registry of Internet Numbers (ARIN) http://www.arin.net/ | whois.arin.net | North America, part of the Caribbean, and subequatorial Africa |
| Asia Pacific Network Information Centre (APNIC) http://www.apnic.net/ | whois.apnic.net | Asia Pacific |
| Réseaux IP Européens Network Coordination Centre (RIPE NCC) http://www.ripe.net/ | whois.ripe.net | Europe, Middle East, Central Asia, and African countries north of the equator |
| Latin American and Caribbean Internet Addresses Registry (LACNIC) http://lacnic.net/ | whois.lacnic.net | Latin America and Caribbean |

Table 1-1. Four Regional Internet Registries (RIRs)
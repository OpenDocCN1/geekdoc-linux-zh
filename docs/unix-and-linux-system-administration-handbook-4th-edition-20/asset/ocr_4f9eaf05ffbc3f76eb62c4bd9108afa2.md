# Configuration files

behavior for the missing items. Table 17.9 lists the available statements, the Page column points to our discussion of each statement in the upcoming sections.

# Table 17.9 Statements used in named.conf

| Statement | Page | Function |
|---|---|---|
| include | 602 | Interpolates a file |
| options | 602 | Sets global configuration options/defaults |
| acl | 609 | Defines access control lists |
| key | 609 | Defines authentication information |
| trusted-keys | 610 | Uses preconfigured cryptographic keys |
| server | 610 | Specifies per-server options |
| masters | 611 | Defines a list of masters for stub and slave zones |
| logging | 612 | Specifies logging categories and their destinations |
| statistics-channels | 612 | Outputs real-time statistics in XML |
| zone | 612 | Defines a zone of resource records |
| controls | 615 | Defines channels named with rndc |
| view | 617 | Defines a view of the zone data |
| lwres | | Specifies that named should be a resolver, too

Before describing these statements and the way they are used to configure **named**, we need to describe a data structure that is used in many of the statements, the address match list. An address match list is a generalization of an IP address that can include the following items:

+   * An IP address, either v4 or v6 (e.g., 199.165.145.144)
* An IP network specified with a CIDR netmask (e.g., 199.165.16/15)
* The name of a previously defined access control list (see page 609)
* The name of a cryptographic authentication key
* The ! character to negate things

Address match lists are used as parameters to many statements and options.

```
{ 1.2.3.13; 1.2.3/24; \
 128.138.16/24; 198.11.16/24; 204.228.69/24; 127.0.0.1; };
```

The first of these excludes the 1.2.3.13 but includes the rest of the 1.2.0/24 network; the second defines the networks assigned to the University of Colorado. The braces and final semicolon are not really part of the address match lists but are included for illustration; they would be part of the enclosing statement of which the address match lists are a part.

When an IP address or network is compared to a match list, the list is searched in order until a match is found. This "first match" algorithm makes the ordering of

18. CIDR netmasks are described starting on page 460.
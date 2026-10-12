Note that by creating different views of these zones, different information will be returned to queries, depending on where the queries come from. For example, when someone from the Internet requests the address of the DNS server (`ns1.yourdomain.com`), they will get the address `123.45.67.89`. However, when a query for `ns1.yourdomain.com` comes from inside the LAN, the address `10.0.0.1` is returned. Also, any queries from the Internet for addresses of private computers (`red.yourdomain.com`, `blue.yourdomain.com`, and so on) are rejected.

# Editing /etc/named.conf

To begin, you configure the `/etc/named.conf` file on the primary master DNS server representing your example `yourdomain.com` domain. This example starts from the `/etc/named.conf` file that comes with the caching-nameserver package in Red Hat Linux. (Make sure that you install the caching-nameserver and bind packages before you continue.) Following are a few tips relating to editing the `named.conf` file:

+   * If a statement contains substatements, make sure that you end the last substatement with a semicolon.
+   * Comments can appear in the same formats that popular programming languages use. These languages include C (begin with `/∗` and end with `∗/`), C++ (begin with `//` and go to the end of the physical line), and shell or Perl styles (begin from a `#` and go to the end of the physical line).
+   * A leading exclamation mark (!) negates an element. Putting `!123.45.67.89` in a statement causes the IP address `123.45.67.89` not to match the element. (Just make sure that the negation occurs before a positive match or the positive match takes precedence.)

The edited version of the `/etc/named.conf` file is as follows:

```
```
options {
  directory "/var/named";
};

acl "mylan" {
  127/8; 10.0.0.0/24;
};

view "inside" {
  match-clients { "mylan"; };
  recursion yes;

  zone "." IN {
    type hint;
    file "named.ca";
  };

  zone "0.0.10.in-addr.arpa" IN {
    type master;
    file "yourlan.db";
```

```
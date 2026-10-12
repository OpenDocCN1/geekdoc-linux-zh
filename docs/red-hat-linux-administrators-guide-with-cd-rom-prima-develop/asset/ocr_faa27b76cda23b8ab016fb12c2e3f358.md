# Configuring Reverse Entries

Reverse DNS entries provide a means of looking up a domain name by IP address. Rather than looking for a specific domain, if you know the IP address of the box in question, you can then find out the domain name attached to that IP address. These files are usually cataloged by the class IP address. For example, based on the configuration discussed in the preceding section, the name of the reverse file containing gnucware.com would be db.205.82.148. In this manner, the IP address is mapped to the proper domain name.

Another important file in addition to the default reverse IP file resides within the /var/named directory: the db.127.0.0 or localhost lookup file. This file provides the name server with a localhost entry. The syntax is nearly the same as that of the script shown in Listing 15.7, except that this script provides a Reverse Names section instead of a Canonical Names section. Substituting for the host-name is the last number, in this case 1, which then becomes 127.0.0.1. This is usually the first line of the configuration file that specifies specific IP addresses.

Here is the line as it would appear in the db.127.0.0 file:

```
1 IN PTR localhost.
```

Be certain to include a dot or period after the end of localhost. This entry maps the address to the name of the server.

The file for your class C domain, such as 205.82.148, might have the entries indicated in Listing 15.8.

# Listing 15.8 A Sample DNS Reverse Entry for the 206.81.148 Class C Domain

```
;; ============================================================
;; REVERSE RECORD FOR : 205.82.148
;;
;
; Date: Who: What:
;
; 09/20/00 Kerry Cox Updated DNS Entries
; 09/25/00 Kerry Cox Added new servers
;
;; ============================================================
```
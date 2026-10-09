```
;; QUESTION SECTION:
;22.128.157.209.in-addr.arpa. IN PTR
;
;
;ANSWER SECTION:
;22.128.157.209.in-addr.arpa. 2204 IN PTR www.sobell.com.
; ...
```

Alternatively, you can just use host:
```
$ host 209.157.128.22
22.128.157.209.in-addr.arpa domain name pointer www.sobell.com.
```

# # How DNS Works

Application programs do not issue DNS queries directly but rather use the **gethostbyname()** system call. How the system comes up with the corresponding IP address is transparent to the calling program. The **gethostbyname()** call examines the **hosts** line in `/etc/nsswitch.conf` (page 475) to determine which files it should examine and/or which services it should query and in what order to obtain the IP address corresponding to a domain name. When it needs to query DNS, the local system (i.e., the DNS client) queries the DNS database by calling the resolver library on the local system. This call returns the required information to the application program.

# # MORE INFORMATION

+   - **DNS** for Rocket Scientists is an excellent site that makes good use of links to present information on DNS in a very digestible form. The same information is available in the *Pro DNS and BIND* book.
+     - Local: *Bind Administrator Reference Manual*: `/usr/share/doc/bind9-doc/arm/Bv9ARM.html`.
+     - Web: DNS for Rocket Scientists: www.zytrac.com/books/dns
+     - BIND: www.isc.org/products/BIND
+     - DNS security: www.sans.org/reading_room/whitepapers/dns/1069.php (downloadable PDF file)
+     - HOWTO: *DNS HOWTO*
+     - Book: *DNS & BIND*, fifth edition, by Albitz & Liu, O'Reilly & Associates (May 2006)
+     - *Pro DNS and BIND*, first edition, by Ron Aitchison, Apress (August 2005)

# # Notes

+   - **Terms of DNS and named**: The name of the DNS server is **named**. This chapter uses “DNS” and “**named**” interchangeably.
+   - **Firewall**: The **named** server normally accepts queries on TCP and UDP port 53. If the server system is running a firewall, you need to open these ports. Using **gufw** (page 876), open this port by setting a policy that allows service for DNS.
+   - **chroot jail**: The **bind-chroot.sh** script sets up **named** to run in a chroot jail. After you run this script, all files that control BIND are located within this jail. In this case the file-names used in this chapter are symbolic links to the files in the chroot jail. See page 847 for more information.
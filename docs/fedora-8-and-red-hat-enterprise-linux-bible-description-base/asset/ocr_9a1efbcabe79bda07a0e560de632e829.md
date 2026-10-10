# ## Getting a domain name

Domain names are available from dozens of different domain registrars these days. You can check the availability of domain names from any of these registrar’s Web sites, such as GoDaddy (godaddy.com) or Network Solutions (networksolutions.com). You can also use the whois command that comes with Fedora and RHEL.

The top-level domain (TLD) in which you register your own domain should reflect the type of business or organization that you represent. Commercial businesses typically use the .com TLD. Newer TLDs, however, such as .biz and .info, are now available for domains that represent a business community or for information about businesses and individuals. Some people choose .ws to represent their Web site, although the .ws TLD is actually owned by the government of Western Samoa, which agreed to license it as a general-purpose Web site domain.

Other common TLDs are .net (originally for network services companies) and .org (originally intended for organizations). Although those domains were intended for special purposes, there are really no restrictions on who can get and use those domain names.

Institutions of higher education in the United States use the .edu TLD. A TLD that has recently become available for public use is the .us TLD, for organizations within the United States (public K-12 schools in the U.S. typically use the .us TLD). Countries outside of the United States each already have their own TLD.

# ## Checking domain name availability

With an active Internet connection, you can use the whois command in Red Hat Linux to check if a domain name is available in the .com, .net, .org, or .edu domains. Following is an example of using whois to check the availability of the domain handsonhistory.com:

```
$ whois handsonhistory.com
[Querying whois.internic.net]
.
.
.
Registrant:
Hands-On-History (HANDSONHISTORY-DOM)
PO Box 943
Port Angeles, NJ 98221
US

Domain Name: HANDSONHISTORY.COM
.
.
.
Technical Contact:
Support domains@XMISSION.COM
Xmission Domain (XDS)
```
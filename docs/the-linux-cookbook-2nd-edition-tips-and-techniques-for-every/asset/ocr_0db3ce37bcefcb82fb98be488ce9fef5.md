⇒ To find the hostname that corresponds to the IP address 152.2.210.81, type:

```
$ dig -x 152.2.210.81 [RET]
...output messages...
;; ANSWER SECTION:
81.210.2.152.in-addr.arpa. 1D IN PTR metalab.unc.edu.
...output messages...
$
```

In this example, dig output that the FQDN corresponding to the given IP address was metalab.unc.edu.

# 34.6.5 Listing the Owner of a Domain Name

An Internet domain name's domain record contains contact information for the organization or individual that has registered that domain. Use the whois command to view the domain records for the common .com, .org, .net, and .edu top-level domains.

With only a domain name as an argument, whois outputs the name of the "Whois Server" that has that particular domain record. To output the domain record, specify the Whois Server to use as an argument to the -h option.

⇒ Here are two ways to use this.

+   - To output the name of the Whois Server for columbia.edu, type:
+     $ whois columbia.edu [RET]
+   - To view the domain record for columbia.edu, using the whois.educause.net Whois Server, type:
+     $ whois -h whois.educause.net columbia.edu [RET]

NOTES: This command also outputs the names of the nameservers that handle the given domain—this is useful to get an idea of where a particular Web site is hosted.

# 34.7 Chatting with Other Users

There are several ways to interactively chat with other users on the Internet, regardless of their platforms or operating systems. The following recipes describe the most popular tools and methods for doing this.
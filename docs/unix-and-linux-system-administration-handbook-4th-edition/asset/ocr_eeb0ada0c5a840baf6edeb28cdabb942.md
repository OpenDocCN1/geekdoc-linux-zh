Let's dissect that record in a bit more detail:

+   - v=spf1 indicates that the record conforms to version 1 of the SPF protocol, described in RFC4408. v=spf2.0 would indicate Microsoft's Sender ID system, described in RFC4406.
+   - The ip4 tags indicate that the following data value is a normal IP network or host address. Multiple clauses can be included, as is done here.
+   - ?all indicates "done" to the checking function that interprets the record.

The complexity of the full SPF language is disheartening. Other tags are available to list hostnames, MX records, PTR records, IPv6 addresses, and so on. Some of these forms require a second DNS lookup, so although they may add convenience or flexibility, they are less efficient than the ip4 tag. The examples at the end of RFC4408 are a good reference if you want to get fancy with your SPF records.

Here is another example, obtained with dig sendmail.com txt:

```
sendmail.com.      IN  TXT "v=spf1 ip4:209.246.26.40 ip4:209.246.26.41 ip4:63.211.143.38 ip4:209.246.26.36 ip4:209.246.26.39 ip4:209.246.26.24 ip4:209.246.26.25 ip4:209.246.26.10 ip4:209.246.26.53 ip4:72.32.154.224/27 ptr:constantcontact.com ~all"
```

This record specifies complete server IP addresses rather than entire networks. At the tail end of the IP address list is a ptr: clause that permits constantcontact.com to send mail purporting to be from sendmail.com. This clause should only take effect if constantcontact.com has a matching PTR record, which isn't currently the case—as of this writing, the PTR maps back to www.constantcontact.com, not constantcontact.com. Either email receivers are not checking the PTR record rigorously or the SPF record has a small bug.

Surveys (sendmail.org/dkim/survey) of about 1,000 U.S. banks and Fortune 1,000 companies showed that SPF was supported by more than 90% of the sites, with the Sender ID format being used by only 1%–2%. Some email readers (e.g., Gmail) print a bright red warning banner across a message that has failed an SPF check and might be phishing.

sendmail, Postfix, and exim support SPF processing; Microsoft Exchange supports Sender ID. See page 768 for more SPF information.

# DKIM and ADSP records

DKIM stands for DomainKeys Identified Mail and is a merge and enhancement of two systems: DomainKeys from Yahoo! and Identified Internet Mail from Cisco. It's a signature system for email. The receiver of a message can authenticate the sender (no forgeries) and guarantee the message's integrity (no meddling).

A lot of work has gone into the DKIM specifications so that edge cases like mailing lists and outsourced email solutions will work correctly. Another focus of the DKIM design is to make implementation easy; it requires no per-user or per-host

> DKIM records are specified in RFCs. 4871 (2007) and 5617 (2009).
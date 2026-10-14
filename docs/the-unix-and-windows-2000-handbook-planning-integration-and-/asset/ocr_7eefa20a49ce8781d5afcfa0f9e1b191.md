pilots.sniglets.com You can have as many CNAME entries as you would like mapped to a single A record. You can even have CNAME entries mapped to other CNAME entries. However, be aware that you can only have one A record for each distinct IP address.

> A records are a one-to-one mapping, with only one A record for each distinct IP address. You may have as many CNAME entries as you like associated with a single A record. You may also associate CNAME entries with other CNAME entries.

![](bbox=[0.08, 0.24, 0.18, 0.31])

With an understanding of the SOA, NS, A, and CNAME records, you can build a functional zone. However, there are two more resource records that you will find useful when creating your master DNS information. If we look back to our entry for pilots.sniglets.com, you first see the MX resource source defined:

```
pilots          IN  A       192.168.3.4

drivers         IN  CNAME   pilots.sniglets.com
                IN  MX      10 mail.sniglets.com.
                IN  MX      20 sniglets.com.
                IN  HINFO   HP710 HP/UX
```

The MX resource defines the SMTP mail exchanger for the entry. Mail exchangers are useful when you want to redirect incoming SMTP mail to a single or well-defined set of SMTP mail servers. In large networks, it is unwise to have each UNIX system function as its own mail server. By using MX records, you provide a mechanism to inform remote SMTP servers where to attempt to deliver mail destined for users at the defined system.

In this example, mail.sniglets.com is the primary SMTP system for pilots.sniglets.com, with system sniglets.com acting as a backup mail server should mail.sniglets.com fail to respond. The integer values in front of the SMTP servers represent a weight, with smaller numbers representing the most preferred SMTP server. For more information on configuring your SMTP mail servers, see Chapter 9, "Electronic Mail and Messaging."

The final resource record you'll find useful is the HINFO resource. HINFO provides a way to insert comment information into DNS. The HINFO record is defined as a two-field text record separated by a space. You can use these two fields to insert information about the system, such as system type, operating system level, system owner, or location. This can be very useful if you have a large installation, or if you want to share information through DNS.
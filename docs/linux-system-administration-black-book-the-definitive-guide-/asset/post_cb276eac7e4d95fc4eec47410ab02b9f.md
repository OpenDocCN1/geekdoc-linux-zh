
```
key keyID {
    algorithm algoID;
    secret codelist;
};
```

The available *algoIDs* are Digital Signature Algorithm/Digital Signature Standard (DSA/DSS), Hash Method Authentication Code-Message Digest 5 (HMAC-MD5), and RSA (the first letters of the three inventors' last names). The DSA/DSS algorithm was released in 1994 as the digital authentication standard used by the U.S. government. It is fast at creating new signatures but slow at verifying them, which makes it not always the best choice in a client/server environment. Its cousin, RSA, is just the opposite. It generates signatures slowly, but verifies them quickly. This is one reason RSA is typically chosen over DSA/DSS.

> **NOTE:** *For more on DSA/DSS and RSA, go to www.rsa.com. HMAC is discussed in context in a variety of Requests For Discussion (RFCs) available at www.faqs.org/rfc.*

See the Immediate Solutions section “Creating Encrypted Keys” for assistance in implementing this feature.

Although it is possible to control some aspects of logging with **syslogd**, it is wise to take advantage of server-specific configuration when you can. You can do this with **named** by using the **logging** statement. This particular statement is complex, with many optional pieces to it, so it is broken down some here. It starts, predictably, with the following:

```
logging {
```

The first potential section of a **logging** statement defines one or more channels through which information is passed to a specific place. If you choose to include a **channel** statement, it begins with:

```
channel name {
```

Next, you build one of the following three items: **file**, **syslog**, or **null**. A **file** statement declares a specific file that this channel points to, such as

```
file "path";
```

On the other hand, perhaps you want to have **syslogd** handle the logging. You can do this with the following:

```
syslog who;
severity level;
```

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_354_0.png)

# DNS With BIND

**TIP:** Review Chapter 9’s discussion of logging to refresh your memory of which entities **syslogd** knows and what the severity levels are.

Or, maybe you want to send particular types of data into the great /dev/null void (anything sent here gets discarded). You can do so with the following:

```
null;
```

You can also choose what gets printed. Three items are available for this:

```
print-category value;
print-severity value;
print-time value;
```

In all three cases, the value is either **yes** or **no**. None of these three is necessary. Choose as many or as few as you need. Finally, the **channel** part of the **logging** statement is done, so close it, if you used it, with the following:

```
};
```

The other subsection available in a **logging** statement is **category**, with which you can lump a number of different channels together and specify categories of information that need to be logged. The available categories are listed in Table 11.3.

**Table 11.3** Categories available in /etc/named.conf.

| Category | Logs |
| :------- | :------------------------------------------------------------- |
| **cname** | Messages that list what points to a CNAME value. |
| **config** | Messages pertaining to the configuration file. |
| **db** | Database operations. |
| **default** | What you get if you do not specify categories. Many consider this setting to be sufficient, because it logs **syslog** and **debug** messages. |
| **event** | Messages that pertain to timed events, user-action–initiated events, events opened by other programs, and more. |
| **insist** | Messages pertaining to internal consistency checks. |
| **lame-servers** | Messages pointing out that a server **named** dealt with was not fully compliant with the latest protocols. |
| **load** | Messages pertaining to zone data loading. |
| **maintenance** | Messages pertaining to maintenance routines. |
| **ncache** | Messages regarding failed lookup caching. |
| **notify** | Messages pertaining to the NOTIFY protocol, which is used to send explanations as to why connections failed. |
| **os** | Messages regarding problems with the operating system itself |
| **packet** | Complete dumps of the packets sent and received. This has to point to a file. |
| **panic** | Server panic messages. |
| **parser** | Problems reading /etc/named.conf. |
| **queries** | Messages with summaries of the name service queries received. |
| **response-checks** | Query response error messages. |
| **security** | Authentication requests, both those that succeeded and those that failed. |
| **statistics** | Name service usage statistics. |
| **xfer-in** | Incoming zone transfer information. |
| **xfer-out** | Outgoing zone transfer information. |
| **update** | Information regarding dynamic zone updates. |

A **category** statement looks like this:

```
category catname {
    channelname:
    cat1;
    cat2;
    ...;
    catn;
};
```

Now, finally, you can close your **logging** statement:

```
};
```

The last statement type available in /etc/named.conf is the **server** statement, which is where you tell **named** about servers it accepts and sends zone files to. This statement is used in the following format:

```
server serverIP {
    settings;
};
```

Four settings are available. You can use none of them or any combination of them. The first is the **bogus** setting. This prevents your name server from believing anything the specified name server tells it. You use this item in one of the two following configurations:

```
bogus yes;
bogus no;
```

Next, you can secure your zone files somewhat by using a **keys** setting. You already have to have set up a **key** statement elsewhere. After you have, use the following to implement key-based authentication:

```
keys {
keyID1
keyID2
...
keyIDn
};
```

## The Zone Files

A DNS zone file is where you specifically lay out which IP addresses map to which hosts, and other useful information such as the primary mail servers for your domain. Each entry in this file is called a *resource record*. What types of records, and how many, depend on which zone file you are setting up. This information is given in the context of the tasks in the Immediate Solutions section. This section covers the theory underlying how the file is laid out. One interesting thing to note is that zone files are the same regardless of the operating system you are using. They have to be, because you never know what operating system the organization providing your backup DNS runs its name service under.

A zone file begins with the Start of Authority (SOA) record, which is what you use to lay out overall information about the zone before you get into the details. This statement is laid out in the following manner:

```
@ IN SOA domain.extension. admin.domain.ext. (
serial_number
refresh
retry
expire
minimum )
```

The parts that you do not change are:

- **@**—The zone’s name. The @ is a self-referential wildcard—meaning that it stands for the default domain name.
- **IN**—The protocol group that this domain name belongs to. IN stands for the Internet protocol group, or the Internet class of naming.
- **SOA**—The type of resource record this section of the file represents. SOA stands for the Start of Authority resource record.

After this is the section that you need to customize:

- **domain.extension.**—This zone represents the zone administrator’s email address.

> NOTE: Notice the dot at the end of the extension—this dot must be here. The same goes for the next entry.

- **admin.domain.ext.**—This is the same thing as admin@domain.ext. In this case, the admin item does not refer to a hostname.
- **serial_number**—This entry must change every time you update the zone file. This is what allows your slave servers and other servers that grab copies of the zone to know that a change has been made. The serial number must be in a format that you can increment, and that computers can tell you have incremented. You and the computer both must be able to tell where in the sequence of zone changes this file lies. Some administrators accomplish this by using a date format such as YearMMDD#, which might look like 200010152. The extra number on the end allows for multiple changes on the same day. Other administrators, however, just start at 1 and keep adding. Both methods are legitimate. If you choose any type of complicated scheme, make sure to document it with a comment at the end of the line. For example, if you use YearMMDD#, you might have this comment at the end:

```
200010152 ; YearMMDD#
```

> NOTE: The semicolon, regardless of where it appears in the file, ensures that everything after it is ignored by named when it parses the zone file.

- **refresh**—This expresses how long a slave name server should wait between checks with the master server to see whether this file has changed. You have to enter this in seconds, but this does not mean that the interval has to be short. It depends on how often you tend to change the host information for this zone, and how long you can risk waiting for the zone information to propagate. For a three-hour wait between check-ins, you might use:

```
10800 ; 3 hours
```

- **retry**—This signifies how long the slave name servers should wait to recheck if they try to check for a change and cannot reach the master server. Don’t

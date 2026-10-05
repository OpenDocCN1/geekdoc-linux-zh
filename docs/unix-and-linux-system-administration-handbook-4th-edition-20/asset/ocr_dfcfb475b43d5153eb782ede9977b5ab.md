# Chapter 17 DNS: The Domain Name System

# Resource records

Each zone the DNS hierarchy has a set of resource records associated with it.
The basic format of a resource record is

```
[name] [ttl] [class] type data
```

Fields are separated by whitespace (tabs or spaces) and can contain the special characters shown in Table 17.5.

# Table 17.5 Special characters used in resource records

| Character | Meaning |
| --- | --- |
| : | Introduces a comment |
| @ | The current zone name |
| () | Allows data to span lines |
| * | Wild card* (name field only) for some cautionary statements. |

+   a. See page 584 for some cautionary statements.

The name identifies the entity (usually a host or domain) that the record describes. If consecutive records refer to the same entity, the name can be omitted after the first record as long as the subsequent records begin with whitespace. If it is present, the name must begin in one column.

A name can be either relative or absolute. Absolute names with a dot and are complete. Internally, the software deals only with absolute names; it appends the current domain and a dot to any name that does not already end in a dot. This feature allows names to be shorter, but also invites mistakes.

For example, if cs.colorado.edu was the current domain, the name "anchor" would be interpreted as "anchor.cs.colorado.edu". If you entered the name as "anchor.cs.colorado.edu", the lack of a final dot would still imply a relative name, resulting in the name "anchor.cs.colorado.edu.cs.colorado.edu."—this kind of mistake is common.

The ttl (time to live) field specifies the length of time, in seconds, that the data item can be cached and still considered valid. It is often omitted, except in the root server hints details. It defaults to the value set by the *TTL* directive (see page 596 for format details), which must be the first line of the zone data file.

Increasing the value of the ttl parameter to a week substantially reduces network traffic and DNS load. However, records have been cached outside your local network, you cannot force them to be discarded. If you plan a massive renumbering and your old ttl ttl was a week, lower the *TTL* value (e.g., to one hour) at least a week before your intended renumbering. This preparatory step makes sure that records with long-week ttls are expired and replaced with records that

See Chapter 19 for more information about NIS.
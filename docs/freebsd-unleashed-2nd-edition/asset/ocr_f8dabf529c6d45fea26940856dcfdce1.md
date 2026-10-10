Although it may look as though this is an unformatted mess, there is in fact a distinct structure to it. Listing 31.2 consists of six basic elements:

+   * A $\mathrm{TTL}$ directive
+   * The SOA (Start of Authority) record
+   * A block of NS (Name Server) records
+   * A block of A (Address) records
+   * A block of CNAME (Canonical Name) records, which define aliases
+   * An MX (Mail Exchanger) record

Aside from the directives, each element of the file is a resource record (RR), defining the properties of a name within the zone relative to a certain "origin." The following sections look at each of these elements in turn.

# ### Directives

The zone file format allows for a number of different basic directives. These are global settings for the entire file, and each one is specified in capital letters beginning with a dollar sign ($). Directives can appear anywhere in the zone file, and each subsequent directive of the same type overrides any previous ones.

Of all the available directives, only $\mathrm{ORIGIN}$ is generally very useful in practice:

+   * $\mathrm{ORIGIN}$—Syntax: $\mathrm{ORIGIN}<\$domain-name>\[<\$comment>]$

$\mathrm{ORIGIN}$ is what will be appended to any unqualified name in a record. An unqualified name is, for instance, www; if www is listed in a record in a zone file with the $\mathrm{ORIGIN}$ directive set to somewhere.com., the record will be defined as www.somewhere.com. (with the trailing dot).

If $\mathrm{ORIGIN}$ is not set within the zone file, it is assumed to be the same as the name of the zone specified in the zone statement that refers to it. If an $\mathrm{ORIGIN}$ directive doesn't have a trailing dot, it is not "absolute," meaning that it will be appended to any previous $\mathrm{ORIGIN}$ strings. For example, the directive

```
$
ORIGIN com.
ORIGIN somewhere
www IN CNAME stripes
$
```

is equivalent to

```
$
www.somewhere.com. IN CNAME stripes.somewhere.com.
$
```

Be careful when handling these trailing dots! If your domains are not resolving properly, check the dots first and make sure your $\mathrm{ORIGIN}$ statements combine to the proper string.
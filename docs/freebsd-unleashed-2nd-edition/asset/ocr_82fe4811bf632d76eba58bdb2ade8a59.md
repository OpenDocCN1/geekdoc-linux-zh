+   - **$INCLUDE**—Syntax: $INCLUDE <filename> [<origin>] [<comment>]

The $INCLUDE directive imports the file specified by <filename> and processes it as if it were a part of the zone file at the point where $INCLUDE appears. For the duration of the included file, $ORIGIN is set to <origin> if specified.

+   - **$TTL**—Syntax: $TTL <default-ttl> [<comment>]

$TTL sets the default time-to-live (in seconds) for any records where the TTL value is not set. Generally, this is useful only for such things as *negative caching*, where BIND caches the fact that a record *does not* exist for a certain period (in other words, the TTL). In a resource record (RR), the TTL is the field that appears before the class column—blank in the records shown in Listing 31.2 (the IN field is the class). These records inherit the value of $TTL shown at the top of the listing, which is 3600 seconds in the example.

+   - **$GENERATE**—Syntax: $GENERATE <range> <1hs> <type> <rhs> [<comment>]

$GENERATE is used to create a range of records that differ by an *iterator*, or a step value. In other words, you can automatically specify a large list of name records whose names and mapped IP addresses fit a certain formula:

+   - **<range>**—This can be one of two forms: *start-stop* or *start-step/step*. If the first form is used, *step* is set to 1.

+   - **<1hs>**—This describes what will vary between the newly created records on the left-hand side of the record. Any single $ symbol within the left-hand side is replaced by the iterator value. If <1hs> is not an absolute name, the current $ORIGIN is appended to it. Use a 0 as a placeholder if nothing on the left-hand side should be iterated.

+   - **<type>**—Can be any one of PTR, CNAME, or NS.

+   - **<rhs>**—Does the same as <1hs>, except for the right-hand side of the record.

The $GENERATE directives

```
    $ORIGIN 0.0.192.in-addr.arpa.
    $GENERATE 1-2     0 NS    ns$2.somewhere.com.
    $GENERATE 1-127 $ CNAME $0
```

are expanded by BIND into the following:

```
    0.0.0.192.in-addr.arpa. NS    ns1.somewhere.com.
    0.0.0.192.in-addr.arpa. NS    ns2.somewhere.com.
    1.0.0.192.in-addr.arpa. CNAME 1.0.0.0.192.in-addr.arpa.
    2.0.0.192.in-addr.arpa. CNAME 2.0.0.0.192.in-addr.arpa.
    ...
    127.0.0.192.in-addr.arpa. CNAME 127.0.0.0.192.in-addr.arpa.
```
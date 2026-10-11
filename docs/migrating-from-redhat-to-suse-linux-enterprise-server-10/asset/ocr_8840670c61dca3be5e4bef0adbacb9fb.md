# # Configure the Lookup Tables

Lookup tables contain rules for processing email within the overall Postfix system.

These tables are activated by variables in the file

```
`/etc/postfix/main.cf`
```

The tables are then defined as

```
`/etc/postfix/lookup-table`
```

After a lookup table has been defined, it needs to be converted to the required format (usually in the form of a hash table) using the command **postmap**.

This is done by entering:

```
```postmap hash:/etc/postfix/lookup-table```
```

The structure of lookup tables is subject to the following general rules:

+   - Blank lines or lines that begin with a # are not interpreted as command lines.
+   - Lines that begin with a space are regarded as a continuation of the previous line.

It is also possible to use regular expressions.
Instead of domain names, you also can use IP addresses.

> > A man page exists for every lookup table: **man 5 lookup-table**.
```
# cat New_Events.evt | evmpost -r -M | evmshow -D
```

# 8.7.13 How Can I Sort the Events?

Since events can come from a variety of channels, the order in which they are displayed is not always the order in which you may expect to see them. Furthermore, you may wish to see the events sorted by different data items. The evmsort command was designed to accomplish this task.

# NOTE:

As of Tru64 UNIX version 5.1, the evmget command automatically invokes the "evmsort -A" command when the "-A" switch is used.

To sort events, you use the "-s" switch followed by a "Sort-Spec". The "Sort-Spec" is defined as a colon (:) delimited string of EVM data types. The sort order is determined by placing either a "+" or "-" after an EVM data type in the "Sort Spec" (the "+" indicates an ascending sort order while a "-" indicates a descending sort order). If you do not specify the sort order it will default to ascending order.

For example:

```
@timestamp+:@name:@priority-
```

This sorts each event by the timestamp (in ascending order), then by the name (in ascending order), and then by priority (in descending order).

The following examples will deliver the same results.

```
# evmget | evmsort -s "@timestamp+:@name:@priority-" | \
> evmshow -t "@timestamp [@priority] @name"
```

Or:

```
# evmget | \
> evmsort -A -s "@timestamp+:@name:@priority-" -t "@timestamp [@priority] @name"
```

Or:

```
# evmget -A -s "@timestamp+:@name:@priority-" -t "@timestamp [@priority] @name"
```
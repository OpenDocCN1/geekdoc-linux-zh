
Even if you don’t use the metric clause, you need the open curly brace. Now drop down to the next line. You start this one with the information that specifies what exact route to which you’re referring. As usual, you can have multiple lines here in the format:

```
route1;
...
routeN;
};
```

If you don’t want to use the default metric, you have the usual two options for the end of each line (before the semi-colon):

- metric value. Set the cost for using this interface instead of using the default costs of 0 for direct, 40 for kernel, or 60 for static.
- restrict. Do not allow routes matching this rule to be exported.

## Configuring Route Aggregation

As we discussed in Chapter 4, you can advertise a network address to the outside world as though it is a single-piece entity, when in fact it is broken down into smaller networks with subnets or IPv6. As long as gated, your router, understands where to send the data once it reaches the overall network, everything will work fine.

You start a route aggregation section with one of the following lines of code:

```
aggregate default
aggregate networkIP
aggregate networkIP mask netmask
aggregate networkIP masklen bitmask
```

You should already be familiar with the terms networkIP, netmask, and bitmask by this point. The second line also has a number of combinations you might use:

```
{
preference value {
brief {
preference value brief {
```

- static. This rule applies to routes assigned with a static gated statement.
- value. This rule applies to the specified routing protocol out of those supported by gated.

Another item available for placing after proto (with or without what you see in the preceding list) is a choice of one of the following:

- as asnum. This rule applies to the specified autonomous system.
- as asregexp. This rule applies to the autonomous systems that match the regular expression.
- tag value. This rule applies to the routes that have the specified tag.

Now is when you decide where you're going with this rule. If it is only meant to prevent a single aggregation, just end it with:

```
restrict;
```

However, if you want to build a series of rules according to what networks and hosts you're looking at, then you next have to decide if you want to use the default aggregate preference value of 130 or if you want to change it for this rule as an overall new default. If you do, start the next line with:

```
preference value {
preference value
```

If not, just use the curly brace on this line. On the next line, you use the very familiar format:

```
route1;
routeN;
```

```
};
```

As usual, with each route you can add at the end either restrict or preference value. Build as many proto statements as you need within the overall aggregate statement, and then close it all out with an ending:

```
};
```

## Running Public gated

Fortunately, the most complex part of dealing with gated is the configuration. After you reach the point of actually being ready to run the daemon, it's time to make sure that the router is working as you anticipated. Only then can you finally rest. What I recommend here is typing things manually at the command line and taking notes for what works and what doesn't. As soon as you know the exact format you need to use when running gated, add the command to /etc/rc.local or to the daemon init script according to how you prefer to start your network services.

As a general rule, you don't tend to work directly with gated at this point. One of this daemon's companion programs is gdc, which is the gated controller. Even if you've already installed gated, you might not have gdc. It seems that some distributions don't include gdc as part of the gated package, nor even in a separate one. However, gdc does come with the main gated public source, which you can get by going to www.gated.org.

## Starting gdc

The gdc program itself doesn't run continuously. Each time you want to use it, you have to use the necessary flags and commands. The flags are listed in Table 5.25. As soon as you have gdc and its flags typed in, add the commands specified in the following section. This allows you to manipulate gated without having to actually touch the daemon itself. Doing this can save a lot of angst and heartache down the road.

| Table 5.25 Command-Line Switches Available When Starting gdc |
|---|---|---|---|
| Flag | Purpose | Format | Value(s) |
| -c | Sets the maximum allowed size of a gated coredump—only when gated is started using gdc. | -c size | Size in bytes. |
| -f | Sets the maximum allowed size of a gated state dump file—only when gated is started using gdc. | -f size | Size in bytes. |
| -m | Sets the maximum allowed data segment size for gated—only when gated is started using gdc. | -m size | Size in bytes. |
| -n | Sets gated to not alter the kernel forwarding table. | -n | N/A |
| -q | Sets gated to run in quiet mode, sending nothing to STDOUT. Error messages are logged according to settings in syslog.conf. | -q | N/A |

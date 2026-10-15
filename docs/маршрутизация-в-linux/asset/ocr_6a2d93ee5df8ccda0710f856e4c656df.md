+   - static. This rule applies to routes assigned with a static gated statement.
+   - value. This rule applies to the specified routing protocol out of those supported by gated.

Another item available for placing after proto (with or without what you see in the preceding list) is a choice of one of the following:

+   - as asnum. This rule applies to the specified autonomous system.
+   - as asregexp. This rule applies to the autonomous systems that match the regular expression.
+   - tag value. This rule applies to the routes that have the specified tag.

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

# Running Public gated

Fortunately, the most complex part of dealing with gated is the configuration. After you reach the point of actually being ready to run the daemon, it's time to make sure that the router is working as you anticipated. Only then can you finally rest. What I recommend here is typing things manually at the command line and taking notes for what works and what doesn't. As soon as you know the exact format you need to use when running gated, add the command to /etc/rc.local or to the daemon init script according to how you prefer to start your network services.
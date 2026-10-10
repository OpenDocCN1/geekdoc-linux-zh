# tracepath

**Purpose:** Display TCP/IP routing information on Linux systems.

**Usage syntax:** `tracepath [OPTIONS] [HOST]`

![](bbox=[0.14, 0.2, 0.93, 0.42])

The **tracepath** command is a replacement for the **traceroute** command on Linux systems. You can use either program on Linux, but many distributions only include **tracepath** by default. The above example demonstrates using **tracepath** to display the route to www.google.com.

> **Tip** *The* `tracepath6` *command is used to trace IP version 6 hosts.*

Common usage examples:

```
```bash
tracepath [HOST]
```
```

Trace the path to the specified host

```
```bash
tracepath -n [HOST]
```
```

Do not lookup DNS names when tracing
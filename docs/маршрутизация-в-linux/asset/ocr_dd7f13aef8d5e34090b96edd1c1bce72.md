# Table 5.24 Continued

| Option | Purpose | Format | Value(s) |
|---|---|---|---|
| retain | Do not erase this route from the kernel's route forwarding tables during shutdown. | retain | N/A |

# Configuring Route Importation

Your routers don't just advertise your network's information to the Internet or external networks. They also receive advertisements from the outside containing vital data for directing packets from place to place. This data is not just collected blindly into a routing table by gated. You have to set up the rules for how the importation of routes operates on each gated router.

The gated.conf file allows you to set up different rules for each protocol type. They're covered here in the order they were covered in Chapters 1 and 3. That means the first item of interest is how you set up how RIP routes are imported.

You start the RIP import statement in the following format:

```
import proto rip
```

From here, you might prevent routes from being imported from other routers using the following structures:

+   - restrict; Do not install any RIP routes matching in the routing table.

+   - interface ilist restrict; Do not install any RIP routes that match ilist in the routing table. To build ilist: use all if you want to match everything; the format xxx.xxx.xxx.xxx to match a full IP address; the formats xxx.xxx.xxx.*, xxx.xxx.*, or xxx.* to match partial IP addresses; eth* to use a wildcarded device name; or the full name of the device such as eth0.

+   - gateway glist restrict; Do not install any RIP routes that match glist in the routing table. To build glist, use the same rules as discussed previously but apply them to the gateways that matching data packets would travel through rather than the interface from which they were first sent.

Alternatively, you might instruct gated to import routes in a similar fashion. Once again, it starts with:

```
import proto rip
```

After this you have one of two options:

+   - interface ilist. Install RIP routes that match ilist in the routing table.

+   - gateway glist. Install any RIP routes that match glist in the routing table.
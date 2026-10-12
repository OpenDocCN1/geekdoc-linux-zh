# ## 21.5 Client browsing more than one domain

We said in the previous module that the retrieved browse list contains details for a single domain only. How then does Windows Explorer show information from multiple domains? To explain this, first let’s look at the **net view** command. This is a command line semi-equivalent of Windows Explorer; it’s advantage is that makes it easier to see exactly what’s happening. We’ll start with three basic variants of the command:

```
`net view`  *get and display the browse list for my domain*
`net view /domain`  *get and display the list of domain names*
`net view /domain:dname`  *get and display the browse list for domain* `dname`
```

(You must leave a space between “view” and “/domain.”) These commands reflect very closely how browsing works internally (and are what we used to generate the network traffic in the previous module). In Figure 21.6 (run on AliceNT, who is part of the TEST-NTD domain), you can see that **net view** without any arguments displays only the machines in this domain.

![](bbox=[0.32, 0.35, 0.68, 0.66])

Displaying information for other domains is a two-step process:

+   1. retrieve a list of domains (**net view /domain**)
+   2. then for each domain, list the machines within it (**net view /domain:dname**).

You can see the outputs for these commands too in Figure 21.6. Our test network has two real domains (UIT and TEST-NTD); the WORKGROUP domain is a hangover from some Samba (Module 22.4) machine.

Figure 21.7, which is a slightly different view of the same data from the previous module, shows the traffic in response to **net view /domain** and **net view /domain:uit** commands. In this example, AliceNT isn’t using WINS.

Lines 184–185 get the list of domain names from my browse master. (The NetServerEnum2 request can be used to get a list of domains as here, or a list of servers as we saw in the previous module, by specifying appropriate flags in the request.)
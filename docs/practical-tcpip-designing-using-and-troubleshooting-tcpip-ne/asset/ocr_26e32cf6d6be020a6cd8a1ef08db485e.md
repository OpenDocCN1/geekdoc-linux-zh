+   3. using the DNS to resolve NetBIOS names (not DNS names)
+   4. the hosts file
+   5. the LMHOSTS file
+   6. an internal cache of names already looked up.

Originally, broadcasting was the only mechanism available. The others were added at different times for performance reasons and to handle the more complex networks that were being used, with routers and WAN/Internet links.

PCs can use different subsets of the six resolution methods and in different orders, depending on how they are configured. We cover that configuration in Module 19.5, along with why you would want each different configuration option and when to use it. First we'll explain what each method is and how it works, in Module 19.3 onwards.

# ## The nbtstat command

**nbtstat** (“NetBIOS status) displays the “name table” for a machine, i.e. the list of names that the machine has registered. **nbtstat** has three different name-display options (as well as other options that we'll see later):

| show my own **name** table | nbtstat -n |
| show name table for hostname *name* | nbtstat -a *name* |
| show name table for IP number *a.b.c.d* | nbtstat -A *a.b.c.d* |

The “A” in “-a” and “-A” stand for *adapter status*, which is an old NetBIOS term for “the list of NetBIOS names that the specified machine owns”. Figure 19.1 shows typical **nbtstat** listings. (Notice that we don't prefix machine names with \ here; if you say, for example, “ nbtstat -a \hal9000-nt” you'll get an error.)

![](bbox=[0.3, 0.61, 0.61, 0.92])

**Figure 19.1 Typical nbtstat listings**
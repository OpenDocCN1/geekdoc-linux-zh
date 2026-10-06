# Part IV ♦ Implementing Network Services in SUSE Linux

Take our domain of palmcoder.net — we control all the information about the palmcoder.net territory on the Internet, and any mistakes or misconfiguration in DNS are under our control. This takes away a huge management burden from a central authority. With millions of web sites in the world, it would take more than an army of monkeys to smoothly run the Internet.

Even though domain control is up to the masses, a central control still needs to exist to allow everyone to query data in the distributed system. These centrally managed servers are called the root DNS servers. They control the top-level domains (TLDs) of the Internet, and this helps to facilitate the idea of a massively distributed network.

# ## Top-Level Domains

Top-level domains (TLDs) encompass the .com, .net, .org, .co.uk, and other similar domains on the Internet. These top-level domains contain information about lower-level domains in the DNS address space. For example, palmcoder.net is under the control of the .net namespace (not the Microsoft programming architecture!).

In Figure 21-1, you can see that palmcoder.net falls under the administrative domain of the .net TLD.

![](bbox=[0.18, 0.535, 0.848, 0.778])

**Figure 21-1:** Top-level domain organization

There are many top-level domains that serve to segregate the domain name space. Table 21-1 lists some of the most common ones.
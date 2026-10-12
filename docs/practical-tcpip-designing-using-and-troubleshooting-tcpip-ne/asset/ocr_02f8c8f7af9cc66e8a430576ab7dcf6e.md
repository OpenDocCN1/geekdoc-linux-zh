Sales has 64 addresses, Tech has 32 and Ops-self has 16, making 112 in all. The next range size up from this is 128, so out of our total space we allocate a 128-address range to Ops. Later on, out of those 128 addresses we will allocate further sub-ranges of 64 and 32 for Sales and Tech respectively.

Now we can configure the HQ router with a single entry: “route any packets for Ops or any of its sub-nets to the Ops router.” The HQ router doesn't know and doesn't care what the Ops router does in the privacy of its own network: all the HQ router needs to know is “there are 128 addresses behind the Ops router” (Figure 6.18). We can change the size of the Sales or the Tech networks, or add a new Marketing sub-net below Ops, etc. without having to tell any other router about it. We've reduced the number of route entries needed *and* made our network more flexible and easier to manage.

![](bbox=[0.11, 0.31, 0.76, 0.5])

# Figure 6.18 128 addresses behind the Ops router

We complete the calculations in the next module
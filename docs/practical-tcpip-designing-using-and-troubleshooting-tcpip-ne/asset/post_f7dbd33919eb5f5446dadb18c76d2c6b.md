
addresses; it shows only the last byte of the address; the first three bytes can have any value that falls in the A, B or C classes

- here’s a different perspective on sub-netting. By using netmasks you can divide a given IP address range into halves or quarters, or eighths, etc. (a bit like dividing a slab of chocolate or toffee) and a sub-net must consist of only one of these pieces.

## The right way to do it

Let’s put into practice what we learned above. Bob and the other PCs on Bob’s wire must be configured to know that Alice and her friends are not on his local wire: his directly connected range must not include Alice’s range. Therefore, instead of allocating our whole 128-address range to the main network, we must allocate a smaller range, which must be 64, 32, 16, 8, or 4. Therefore, the biggest range we can have on the main network is 64 addresses, either `0.–63` or `64.–127`. In other words, the main network can be at most half the size of our full range. That’s the second surprise.

A direct consequence is that if you want to sub-net your address range, you have to make sure that on your main network you use addresses in at most one half of the range, i.e. all your addresses must be in `0.–63` or they must all be in `64.–127`. If they’re not, you won’t be able to sub-net unless you change the IP numbers of some machines so they do all fall within the correct range.

To correct the network in the previous module, you only need to change the netmasks on the main network machines, from 255.255.255.128 to 255.255.255.192, giving a 64-address range, `0.–63`. All the main-network machines are conveniently within the `0.–63` range, so the configuration will work as soon as you change the netmask on Bob, the near-side (internal interface) of Rupert, and the main-network side of Robert.

**Exercise**: implement the example above on your own network. If you can’t sub-net your real network because it has used IP numbers throughout your whole range and not just half of it, use the private addresses `10.*.*.*` on the test sub-net instead. These machines won’t be able to route to the external Internet, but at least you will have an isolated test network to play with that will cause minimal interference with your live network.

As we mentioned in the previous module, each sub-net must consist of a single range, specified by an IP address and a single netmask. You can’t, for instance, join an eight-address range and a 16-address range to make a 24-address sub-net. Because this can’t be specified with a single netmask, and a normal machine with a single interface has only a single netmask, you would have no way to tell a machine that this is the range of addresses connected directly on its local wire. The result would be that this machine couldn’t ARP all the machines on its local wire and some of the local machines would be unreachable.

The final surprise is that we can make the main network range very small, say eight addresses, from `0` to `7`, and use the rest for sub-nets. This means that we could have the following arrangement: main network = `0.–7`, sub-net-1 = `64.–127`, with all the other little ranges, `8.–15`, `16.–31`, `32.–63` still available for use by other sub-nets later. This is the complete opposite of where we started. We thought we could have a main network containing most of the addresses and a tiny little test sub-net, but that’s impossible. You *can* have a tiny main network and many bigger sub-nets.

## 6.9 Lab – complex sub-nets (1) – planning

As an example of how to plan and implement a whole sub-netted internal network for a whole organization, we’re going to sub-net the hypothetical small company that we mentioned in Module 6.6, using the IP address range 192.0.2.0/24. We’ll take it step by step.

- 1. make a list of the separate networks you require
  - main network, not part of any sub-net (“HQ machines”)
  - human resources department (“HR”)
  - operations department (“Ops”)
    - operations, sub-net for sales (“Sales”)
    - operations, sub-net for technical (“Tech”)
  - finance department (“Fin”)
- 2. draw a diagram of the networks (Figure 6.16)

![](img/a2132b646d336d5f9a21102d6320e537_195_0.png)

- 3. specify the maximum number of hosts for each network
Enter the details as shown in Table 6.1. For each sub-net:
- enter only the number of hosts on that network’s own wire; don’t include hosts in its child sub-nets if it has any, and don’t include any routers, because we do that explicitly in a moment

– even if a network has child sub-nets, the parent network may contain machines that are not in any child network, i.e. that are on its own wire. We’ve labeled these as “-self” to emphasize they are connected locally to the router above (e.g. **HQ-self** for the HQ servers and desktops on the main network, and **Ops-self** for the Operations servers and desktops shown in Figure 6.16). If there are no hosts on the wire, enter zero in the table. (You can’t omit this wire completely from your calculations because it has routers connected to it.)

– allow for reasonable future expansion in the numbers you specify. (We’ve chosen 14, 15 and 8 as example numbers because they’re going to raise interesting issues in a moment.)

- 4. add in “lost IP numbers” and routers

every range loses its lowest and highest IP numbers for use as broadcast addresses (Module 4.10), so add two (shown shaded) to each row.

Each sub-net is connected to at least one router. The number of IP addresses for router connections is the number of children this sub-net has, plus one for connecting to the parent network. (The HQ network’s parent is the Internet.)

**Table 6.1** Host details

| Network | No. hosts | Lost addresses | Routers children | Routers parents | Total addresses | Range size |
|---|---|---|---|---|---|---|
| HQ-self | 10 | +2 | +3 | +1 | =16 | ↝ 16 |
| HR | 8 | +2 | +0 | +1 | =11 | ↝ 16 |
| Ops-self | 6 | +2 | +3 | +1 | =11 | ↝ 16 |
| Sales | 50 | +2 | +0 | +1 | =53 | ↝ 64 |
| Tech | 15 | +2 | +0 | +1 | =18 | ↝ 32 |
| Fin | 14 | +2 | +0 | +1 | =17 | ↝ 32 |

- 5. calculate the range sizes needed

round up from the total number of addresses to the nearest valid range size (8, 16, 32, etc.). (We’ve used the symbol ↝ to indicate rounding up.) At first glance it looked as though the HR and Ops-self subnets could use eight-address ranges, and Fin, Tech and HQ-self could use three 16-address ranges, but that’s not true – because of the two lost IP numbers and the routers. Notice that the HQ-self network is completely full: we can’t even add a sniffer temporarily, or a printer. (In real life that would be a Bad Idea and we’d use a larger range, but we’ll live with it in this example.)

Note that these ranges are only for the machines on each wire. We now have to work out what size a network has to be to accommodate its child sub-nets as well. We cover that in the next module.

## 6.10 Lab – complex sub-nets (2a) – calculate ranges

6. amalgamate parent and child network sizes and recalculate ranges

We start at the deepest level of sub-net and work upwards. But before completing this step, what does it mean and why are we doing it? Consider only the Ops network and its sub-nets, Sales and Tech (Figure 6.17); forget about the HR and Fin sub-nets for now:

![](img/a2132b646d336d5f9a21102d6320e537_197_0.png)

We can divide traffic coming from the Internet to the main Internet router into two types:

- a. packets for locally connected hosts on HQ's own wire. The router forwards these directly, using ARP if necessary
- b. packets for Ops, for Sales, or for Tech. All of these must be forwarded to the Ops router, which takes care of the rest.

That last sentence is crucial: we have to configure the main Internet router to perform this forwarding. We can do that in two ways:

- i. the Bad Way: configure a separate route for each of the three subnets, Ops, Sales, and Tech. This works, but it complicates our configuration and defeats one of the main purposes of sub-netting – keeping configuration details as local as possible and hiding them from higher levels in the sub-net tree (item 5 in Module 6.6). If we change the size of the Tech network, or add another little sub-net below Ops, not only do we have to reconfigure the Ops router (which is reasonable) but we also have to modify the configuration of the HQ router. Having low-level alterations ripple up and require changes at higher levels in this way is a Bad Thing

- ii. the Good Way: we amalgamate the Ops, Sales, and Tech sub-nets into a single range, and configure that single range on the HQ router.

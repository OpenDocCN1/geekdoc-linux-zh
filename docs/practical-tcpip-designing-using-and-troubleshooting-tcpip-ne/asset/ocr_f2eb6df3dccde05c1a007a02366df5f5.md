![](bbox=[0.08, 0.07, 0.45, 0.25])

![](bbox=[0.45, 0.07, 0.85, 0.25])

# Figure 6.7 Entering the second IP address

![](bbox=[0.15, 0.31, 0.8, 0.5])

# Figure 6.8 Use *ipconfig* to verify settings

Your NT network settings are persistent – as usual, check by running *ipconfig*. Now do a “*route print*” to see how adding the extra interface automatically created the necessary routes for you. Figure 6.9 shows two new routes have been added.

![](bbox=[0.23, 0.62, 0.7, 0.75])

# Figure 6.9 Two new routes have been added by adding the 10.2.2.14 address

> **Tip:** in Module 3.7 we recommended that where possible in real life we keep the last byte of all the IP addresses on a router the same, just to make it easy to remember. For example, we would normally have given Rupert the addresses 10.1.1.163 and 10.2.2.163. We didn’t do that here to emphasise that the addresses can of course be completely different.

In the next module we perform the same configuration, but for Linux, and then look at how this modified test network behaves.
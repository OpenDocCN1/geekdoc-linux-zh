# **Method 2 – using ICMP redirects**

Now, more realistically, let's use the flexibility ICMP redirects give us. This allows us to configure special routes only on the routers; host machines only need their single default gateway; ICMP redirects will take care of the rest (Figure 6.4).

![](bbox=[0.06, 0.18, 0.85, 0.44])

(Even without ICMP redirects we could omit the specific routes on Alice, Bob, and Carol and the network would still work. However, every packet travelling to a network on its left would generate twice as much traffic because it would go to its default gateway first and then back to the router on its left.)
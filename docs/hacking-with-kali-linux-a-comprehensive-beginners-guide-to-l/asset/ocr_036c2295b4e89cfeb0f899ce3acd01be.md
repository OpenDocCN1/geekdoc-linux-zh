# What Is Tor, and how does it work?

The Tor network, often referred to as “Tor,” is a volunteer-run system that helps make internet use more anonymous.

When a user is connected to Tor (often through the Tor browser), their outgoing internet traffic is rerouted through a random series of at least three nodes (called relays) before reaching its destination (the website the user wants to visit). Your computer is connected to an entry node, and the final node traffic passes through is the exit node, after which it reaches its destination (the website you want to visit). Incoming traffic is rerouted similarly.

A simplified version of how Tor works (Source: EFF via Wikimedia)

Aside from passing through several nodes, the traffic is encrypted, multiple times in fact. It loses a level of encryption at each node but is never fully decrypted until it leaves the exit node for its destination.

Each node has an identifying IP address, which is also encrypted. The only IP address visible to the destination website is that of the final node, known as the exit node.

In total, the Tor network is currently made up of about 7,000 relays (nodes) and 800 bridges. Bridges are similar to relays, but they are not listed in the Tor directory. They may also be used as a website or app blocks traffic from a detected Tor node.

# Does Tor hide IP address?

While connected to the Tor network, the activity will never be traceable back to your IP address. Similarly, your Internet Service Provider (ISP) won’t be able to view information about the contents of your traffic, including which website you’re visiting.

Your ISP will see that you’re connecting to a Tor entry node, and the website you’re visiting will know the IP address of the Tor exit node.
# ## 8.5 Delegation – tracing the packets

Now we’ll trace a DNS conversation to see how delegation works in practice, and how a server responds to a query for a subdomain that it has delegated. We’ll send a query for the IP address for **www.ibm.com** (use `ping www.ibm.com` ) and follow what happens. In order to see exactly what packets are sent and received, we won’t use our ISP’s name servers at all; instead, we set up a simple name server on our LAN and configure the client PC’s resolver to use that (Figure 8.8).

![](bbox=[0.28, 0.24, 0.78, 0.47])

Figure 8.8 Resolver configuration

There are a few points to note:

+   - as we’ll see in a moment from Figure 8.9, if we didn’t use our own DNS server but relied on the ISP’s instead, we’d miss about 80% of the conversation, because most of it is server-to-server
+   - the resolver configuration, as we saw in the previous chapter, is specific to a PC. We changed the configuration of my PC in Figure 8.8 to use our test DNS server but left all the other PCs alone; they continue to work just as before and don’t even know we have a test DNS server on the network
+   - similarly, the presence of the test DNS server doesn’t affect any other DNS servers we might be running, so we can use the test configuration above on our live network without worrying about breaking our live systems
+   - you may not want to set up a server like this just for exploring how DNS works, and it’s not essential, but if you do want to, we give you some guidance on setting up a server on both Windows-NT (which is easy – see Web Appendix 7) and Linux (Web Appendix 9).

**tcpdump** shows the conversation (below), edited and with line numbers added. **tcpdump**’s standard output format doesn’t contain enough detail for us to work out exactly what’s happening, so we’ll display exactly the same trace in more detail in the next module, and explain it line by line, but for now concentrate on Figure 8.9, which shows the same information diagrammatically.
CAUTION  After you open your server to Internet traffic, break-in attempts will occur. Most will come from automated scripts, sent from infected computers on the Internet. Because CentOS comes with good built-in security features, many attacks bounce off harmlessly. Allowing incoming connections, however, creates vulnerabilities that aren't there with an outgoing-only Internet connection. I strongly recommend that you use security tools, described in Chapter 13, to protect your servers.

# # Determining Goals for Your Server

Before you open up that server sitting in your back office to the Internet, stop for a moment and think about your goals. Here are a few questions that you may want to ask yourself:

+   - How critical is this server for supporting your business?
+   - How much traffic do you expect on your server?
+   - Do you need to support the server 24 hours per day, 365 days per year?
+   - Do you know enough to maintain and secure your server?
+   - Can you get the connection speed that you require at a reasonable cost for your location?
+   - Do you need special equipment, such as an uninterruptible power supply, RAID storage devices, or clustered servers, to ensure continuous service?

Maintaining a public server requires some resources. If the server is critical to your business and in high demand, you may not have the time or expertise to support this server yourself. Also, if no high-speed Internet access is available to your location, even a well-configured server may not have the bandwidth to support your clients.

# # Using a Hosting Service

Tons of places are ready and willing to host your Web content. The number gets a bit smaller, however, if you need to find a place that can help you maintain your CentOS server. In that case, you want to find a company that offers dedicated hosting (i.e., gives you control of an entire server) or permits you to co-locate your server on its premises. In either case, you want to make sure that your server:

+   - Is physically secure.
+   - Can access enough Internet bandwidth.
+   - Has someone there if the server goes down.

You can use such a hosting provider in these ways and still use CentOS as your server:

+   - **Co-locate Your Server at a Hosting Provider or ISP** — In this arrangement, you can get lots of bandwidth and retain your root privileges so that you can still maintain the server yourself. The downside is that the provider probably isn't expected to fix your server if a hardware failure occurs.
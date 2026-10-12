can delegate further if they want. For example, they could set up new domains **sydney.oz.ops.example.com** and **perth.oz.ops.example.com**, each with its own server, and delegate to them. They can do this entirely autonomously, and don't have to refer to us at all (although we would expect them to comply with our corporate naming standard if one has been laid down).

Organizations often delegate large subdomains to individual divisional or departmental control, so that day-to-day modifications of the DNS can be carried out by the people who generate the changes. The delegations typically mirror the organization's structure to a greater or lesser degree.

To summarize, domains are about where names appear in the tree. Zones are related to authority and which server holds the data for a delegated subdomain.

Notice that you can delegate at whatever level you want. We delegated **oz** even though its parent, **ops**, wasn't delegated. And we can delegate at different levels in different places: the **fin** subdomain could be delegated in its entirety, which would give us the structure in Figure 8.7, emphasizing the delegations at different levels.

![](bbox=[0.26, 0.41, 0.75, 0.64])

Figure 8.7 Delegations at different levels

That's the theory of delegation. In the next module we look at it in practice, and use **tcpdump** to see how delegation affects the flow of DNS packets.
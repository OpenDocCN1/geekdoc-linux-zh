# pSeries Communications 249

How is this done? The design of a VPN is a complex undertaking and is the subject of many books and technical papers. Many services organizations, IBM Global Services among them, have the skills and experience to design and manage a VPN project—for a fee, of course. But the basic idea is that techniques called "protocol tunneling" are used, probably in conjunction with encryption. As depicted in Figure 4.4, when a corporation channels its private information via the Internet to remote locations, the information has to pass through many systems not controlled by the company—the dial-up or other Internet access path, the ISP (Internet Service Provider) systems of both sender and receiver, and routers along the way. And that this company's data will be mixed with traffic from thousands of other sources. In the figure, the solid lines represent the physical links among the routers along the way. Routers are designed to optimize the path from the sender to the recipient, and paths through the Internet change all the time. And, without use of special protocols and encryption, there are many points at which a hacker could intercept or at least copy the company's private data.

So a complex set of industry-standard protocols recognized by gateways and routers is used to create a secure “tunnel” (represented by the

![](bbox=[0.19, 0.555, 0.81, 0.863])

Figure 4.4. Conceptual diagram of a Virtual Private Network (VPN).
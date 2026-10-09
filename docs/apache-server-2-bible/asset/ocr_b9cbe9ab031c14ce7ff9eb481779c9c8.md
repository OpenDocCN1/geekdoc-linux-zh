# Understanding encryption

When data travels from one point of the Internet to another, it goes through a number of computers such as routers, gateways, and other network devices. For example, when a visitor to a Web site at www.nitec.com enters his or her credit card number in an HTML form found on the site, it is quite possible that the information travels on a path similar to the one shown in Figure 19-2.

![](bbox=[0.18, 0.28, 0.82, 0.76])

**Figure 19-2:** Data traveling from one point to another on the Internet.

As you can see from the figure, the data must travel through many nodes, so there’s a chance it can be intercepted by someone at one of these nodes. Although data packets travel at a very high speed (usually milliseconds), interception is still a possibility. This is why we need a secured mechanism for exchanging sensitive data. This security is achieved through encryption.
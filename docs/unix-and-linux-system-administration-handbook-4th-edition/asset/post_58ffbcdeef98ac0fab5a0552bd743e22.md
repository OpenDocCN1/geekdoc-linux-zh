
fully featured language such as Java. The common way to interface Java applications to an enterprise’s other data sources is with a “servlet.”

Servlets are Java programs that run on the server on top of an application server platform. Application servers can work independently or in concert with Apache. Most application servers were designed by programmers for programmers and lack the concise debugging mechanisms expected by system administrators. Table 23.3 highlights some common UNIX/Linux application servers.

## Table 23.3 Application servers

| Server | Type | Web site |
|---|---|---|
| Tomcat | Open source | tomcat.apache.org |
| GlassFish | Open source | glassfish.dev.java.net |
| JBoss | Open source | jboss.org |
| OC4J | Commercial | oracle.com/technology/tech/java/oc4j |
| WebSphere | Commercial | ibm.com/websphere |
| WebLogic | Commercial | oracle.com/appserver/weblogic/weblogic-suite.html |
| Jetty | Open source | eclipse.org/jetty |

If you are faced with supporting one of these application servers, seek product-specific documentation and training. Trust us; this is not a technology you can pick up “on the fly” like most UNIX and Linux applications. You’ve been warned.

## Load balancing

It’s difficult to predict how many hits (requests for objects, including images) or page views (requests for HTML pages) a server can handle per unit of time. A server’s capacity depends on the system’s hardware architecture (including subsystems), the operating system it is running, the extent and emphasis of any system tuning that has been performed, and perhaps most importantly, the construction of the sites being served. (Do they contain only static HTML pages, or must they make database calls and numeric calculations?)

Only direct benchmarking and measurement of your actual site running on your actual hardware can answer the “how many hits?” question. Sometimes, people who have built similar sites on similar hardware can give you information that is useful for planning. In no case should you believe the numbers quoted by system suppliers. Also remember that your bandwidth is a key consideration. A single machine serving static HTML files and images can easily serve enough data to saturate an OC3 (155 Mb/s) link.

That said, instead of single-server hit counts, a better parameter to focus on is scalability; a web server typically becomes CPU- or IO-bound before saturating its Ethernet interface. Make sure that you and your web design team plan to spread the load of a heavily trafficked site across multiple servers.

Load balancing adds both performance and redundancy. Several different load balancing approaches are available: round robin DNS, load balancing hardware, and software-based load balancers.

See Chapter 17 for more information about DNS and its behavior.

Round robin DNS is the simplest and most primitive form of load balancing. In this system, multiple IP addresses are assigned to a single hostname. When a request for the web site’s IP address arrives at the name server, the client receives one of the IP addresses in response. Addresses are handed out one after another, in a repeating “round robin” sequence.

Round robin load balancing is extremely common. It is even used by Google. For example, if you query the DNS infrastructure for www.google.com, you might get something like the following records:

```
$ dig www.google.com a
;; QUESTION SECTION:
;www.google.com.          IN  A
;; ANSWER SECTION:
www.google.com.     0   IN  CNAME   www.l.google.com.
www.l.google.com.   65  IN  A       74.125.95.104
www.l.google.com.   65  IN  A       74.125.95.105
www.l.google.com.   65  IN  A       74.125.95.106
www.l.google.com.   65  IN  A       74.125.95.147
www.l.google.com.   65  IN  A       74.125.95.99
www.l.google.com.   65  IN  A       74.125.95.103
```

In this example, the name www.google.com is mapped to the canonical name www.l.google.com. Google adds this layer of indirection so that it can delegate responsibility for content delivery to a downstream provider such as Akamai (see Content distribution networks on page 978 for more context) without giving the CDN control of its root domain.

A DNS client can pick any one of the A records returned for www.l.google.com; it is supposed to do so randomly. Contrary to popular belief, the order in which the A records are returned has no significance. In particular, the first one is not “primary.” Because clients select addresses randomly, the load for this site is distributed roughly evenly across these six servers.

The problem with round robin DNS is that if a server goes down, DNS data must be updated to reroute traffic away from it. Long timeouts on the A records can make this operation tricky and unreliable. On the other hand, short timeouts thwart caching and so make DNS lookups of your site slower and more resource intensive. See Caching and efficiency on page 556 for a discussion of this tradeoff.

In the example above, the A records can be cached for 65 seconds before they expire. That’s a relatively short timeout. If you have a backup server available, you might prefer to use a longer timeout for the A records and to simply reassign a disabled server’s IP address to the backup server.

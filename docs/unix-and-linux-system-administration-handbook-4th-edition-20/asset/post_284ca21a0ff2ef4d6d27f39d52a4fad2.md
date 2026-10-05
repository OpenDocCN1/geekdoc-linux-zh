
# Load balancing

fully featured language such as Java. The common way to interface Java applications to an enterprise's other data sources is with a "servlet."

Servlets are Java programs that run on the server on top of an application server platform. Application servers can work independently or in concert with Apache. Most application servers were designed by programmers for programmers and lack the debugging mechanisms expected by system administrators. Table 23.3 highlights some common UNIX/Linux application servers.

## Table 23.3 Application servers

| Server | Type | Web site |
| --- | --- | --- |
| Tomcat | Open source | tomcat.apache.org |
| GlassFish | Open source | glassfish.dev.java.net |
| JBoss | Open source | jboss.org |
| OC4J | Commercial | oracle.com/technology/tech/java/oc4j |
| WebSphere | Commercial | ibm.com/websphere |
| WebLogic | Commercial | oracle.com/appserver/weblogic/weblogic-suite.html |
| Jetty | Open source | eclipse.org/jetty |

If you are faced with supporting one of these application servers, product-specific documentation and training. Trust us; this is not a technology you can pick up "on the fly" like UNIX and Linux applications. You have been warned.

# Load balancing

It's difficult to predict how many hits (requests for objects, including images) or page views (requests for HTML pages) a server can handle per unit of time. A server's capacity depends on the system's hardware architecture (including subsystems), the operating system it is running, and the extent and emphasis of any system tuning that has been performed, and perhaps most importantly, the construction of the sites being served. (Do they contain only static pages, or must they make database calls and numeric calculations?)

Only direct benchmarking and measurement of your actual hardware can answer the "how many hits?" Questions, people who have built similar sites on similar hardware can give you information that is useful for planning. In no case should believe the numbers quoted by system suppliers. Also remember that your bandwidth is a key consideration. A single machine serving static HTML files and images can easily serve enough to saturate an OC3 (155 Mb/s) link.

That said, instead of single-server hit counts, a better parameter to focus on is scalability; a web server typically becomes CPU- or IO-bound before saturating your Ethernet interface. Make sure that you and your web design team plan to spread the load of a heavily trafficked site across multiple servers.

# Chapter 23

## Web Hosting

Load balancing adds both performance and redundancy. Several different load balancing approaches are available: round robin DNS, load balancing hardware, and software-based load balancers. See Chapter 17 for more information about DNS and its behavior.

Round robin DNS is the simplest and the primitive form of load balancing. In this system, multiple IP addresses are assigned to a single hostname. When a request for the web's IP address arrives at the name server, the client receives one of the IP addresses in response. Addresses are handed out one after another, in a repeating "round robin" sequence.

Round robin load balancing is extremely common. It is even used by Google. For if you query the DNS infrastructure for www.google.com, you might get something like the following records:

### $ dig www.google.com a

```
:: QUESTION SECTION:
;www.google.com.                IN A

:: ANSWER SECTION:
www.google.com.                0 IN CNAME www.google.com.
www.google.com.                65 IN A 74.125.95.104
www.google.com.                65 IN A 74.125.95.105
www.google.com.                65 IN A 74.125.95.106
www.google.com.                65 IN A 74.125.95.147
www.google.com.                65 IN A 74.125.95.999
www.google.com.                65 IN A 74.125.95.103
```

In this example, the name www.google.com is mapped to the canonical name www.google.com. Google adds this layer of redirection so that it can delegate responsibility for content delivery to a downstream provider such as Akamai (see Content distribution networks on page 978 for more context) without giving the CDN of its root domain.

A DNS can pick any of the A records returned for www.google.com; it is supposed to do randomly. Contrary to popular belief, the order in which the A records are returned has no significance. In the first case one is not "primary." Because clients selects addresses randomly, the load for this is distributed evenly across these servers.

The problem with round robin DNS is that if a server goes down, DNS data must be updated to reroute traffic from it. Long timeouts on the A records can make this operation tricky and unreliable. On the other hand, short timeouts thwart caching and so make DNS lookups of your site slower and more resource intensive. Caching and efficiency on page 556 for a discussion of this tradeoff.

In the example above, the A records can be cached for 65 seconds before they expire. A relatively short timeout. If you have a backup server available, might prefer to use a longer timeout for the A records and to simply reassign a disabled server's IP address to the backup server.

## Choosing a server

Load balancing hardware is an alternative to round robin DNS, but it requires some cost. Software-based load balancers are available; Apache is one. Here are some of the factors you may want to consider:

- Robustness
- Performance
- Timeliness of updates
- Availability of source code
- Level of community support
- Cost
- Access control and security
- Ability to act as proxy
- Ability to handle encryption

The Apache HTTP server is "free to a good home," and full source code is available from Apache. The less adventurous may want to install a prebuilt binary package; see the hints in the table below.

## Table 23.4 Locations of Apache

| System | Directory | Recommended source of binaries |
| --- | --- | --- |
| Linux | /usr/sbin | Installed as part of standard distribution |
| Solaris | /usr/apache2 | Installed as part of standard distribution |
| HP-UX | /opt/apache | Install HP-UX 11i "Web Server Suite" |
| AIX | /usr/IBMHS | Install IBM HTTPServer product

# Installing Apache

If you decide to download the Apache source code and compile it yourself, by executing the configure script included with the distribution. This script automatically detects your system and sets up the appropriate makesfiles. Use the --prefix option to specify where in your directory tree the Apache server should live. For example:

```bash
$ ./configure --prefix=/etc/httpd/
```

If you not use configure --help to see the entire list of possible arguments, most of which consist of --enable-module and --disable-module options that include or exclude functional modules that live within the web server.

You can also compile modules into dynamically shared object files by specifying the option --enable-module=shared (or use --enabled-mods-shared-all to make all modules shared). That way, you can decide which modules to include or exclude; only modules you specify in your httpd are loaded at runtime. This is actually the default configuration for the binary-only Apache package—all the modules are compiled into shared objects and are dynamically loaded when Apache starts.

The only disadvantages to using shared libraries are a slightly longer startup time and a very slight degradation in performance (typically less than 5%). For most sites, the benefit of being able to add new modules on the fly and turn existing modules without having to recompile outweighs the slight performance hit.

2003), it's also available as a live CD that runs directly on PC hardware. The live CD is secretly based on Linux, but it does go a long way toward turning a generic PC into a dedicated routing appliance.

# Vendor specifics

Quagga is the go-to routing software for Linux. All of our example distributions either install it by default or make it readily available from the distributor's repository. Quagga has become so entrenched that most distributions no longer include routed. Even where they do, it's a vestigial version without RIPV2 support.

Solaris includes a functional routed (actually called in.routed) that understands RIPV2. It also includes Quagga; you can take your pick. For any sort of IPv6 routing, you'll need to use Quagga.

in.routed is the default routing solution, and it's started automatically at boot time if you haven't specified a default network gateway in the /etc/defaultrouter file. Solaris continues to supply the in.rdisc router discovery daemon, which is curious since its functionality is now included in in.routed.

HP-UX's primary routing system, ramd, is discussed above (see page 524). HP also provides a copy of gated 3.5.9, which is quite old and has no support for IPv6. If you want to manage both IPv4 and IPv6 routing under HP-UX, you'll have to use gated for the former and ramd for the latter. Unfortunately, Quagga does not currently run on HP-UX.

AIX provides three routing daemons: gated v6.0, a routed that speaks only RIPV1, and ndpd-router, an implementation of RIPng and NDP. AIX's gated speaks RIPng, too; however, if you want to use gated for IPv6 routing, you may need to run both gated and ndpd-router. See the documentation for details.

# 15.6 CISCO ROUTERS

Routers made by Cisco Systems, Inc., are the de facto standard for Internet routing today. Having captured over 60% of the router market, Cisco's products are well known, and staff that know how to operate them are relatively easy to find. Before Cisco, UNIX boxes with multiple network interfaces were often used as routers. Today, dedicated routers are the favored gear to put in datacom closets and above ceiling tiles where network cables come together.

Most of Cisco's router products run an operating system called Cisco IOS, which is proprietary and unrelated to UNIX. Its command set is rather large; the full documentation set fills up about 4.5 feet of shelf space. We could never fully cover Cisco IOS here, but knowing a few basics can get you a long way.

By default, IOS defines two levels of access (user and privileged), both of which are password protected. By default, you can simply telnet to a Cisco router to enter user mode.
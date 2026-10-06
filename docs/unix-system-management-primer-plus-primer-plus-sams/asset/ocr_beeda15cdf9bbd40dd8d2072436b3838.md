# UNIX SYSTEM MANAGEMENT PRIMER PLUS

functions can operate without the use of a dedicated server, even if your regular operation devoting ever solely to that use. For example, an authoritative DNS server doesn't need many resources to function; it might easily coexist on the same machine as your mail server. Doubling the functions on a single server during a disaster saves money and eliminates the hassle of installing and maintaining another piece of hardware.

In a reduced DR infrastructure, you should compensate for the fact that you might be overloading the functionality of each machine by asking for more resources than you need. That "breathing room" helps to ensure that the systems can handle all that you throw at them, and it can accommodate future growth, as well. So keep your requests practical; your goal is to plan for a system that can keep critical functions running during a disaster. Exceptional performance is not your first priority in this process. Most customers tolerate a service slowdown that results from a disaster, but they're less likely to tolerate a service that is altogether sluggish.

If you establish a relationship with a disaster recovery partner, they may be able to reserve emergency hardware for you for a recurring fee. Recovery partners are discussed later in this chapter.

# Planning for a Secondary Facility

When planning the resources you'll need to continue data center operations after an emergency, you must include plans for a secondary site of operation. This secondary site is where your technology operations (and potentially your business) will reside during a disaster that incapacitates your primary data center. As you consider the options for procuring your alternative data center, keep in mind that if the online side of your business will be running, as such, you should research and plan it as carefully as you did your primary data center (in Chapter 2).

The three types of secondary sites offer varying levels of disaster readiness:

+   * A cold site is a secondary site that provides the data center, power, HVAC, and other necessary infrastructure. It's not populated with properly configured hardware ahead of time, adding to the minimum recovery time. This is the cheapest secondary site option.
* A warm site provides the data center infrastructure as well as properly configured hardware. The only thing you need to provide for recovery purposes is an up-to-date set of data from backups. A warm site is more expensive than a cold site, but not expensive as a hot site.
* A hot site is a completely functional replica—though on a smaller scale—of your production site, including recent application data. Data is usually mirrored in real-time or copied periodically to the hot site to keep updated with the most current data. In a disaster, you should be able to quickly transition all services to the hot site with little downtime or loss of data. This is the most expensive secondary site option.

Your organization's budget and your tolerance for downtime are the primary factors that will drive your decision on whether to pursue a cold, warm, or hot site. A thorough impact analysis will take these factors into account and determine which type of site is right for your organization.
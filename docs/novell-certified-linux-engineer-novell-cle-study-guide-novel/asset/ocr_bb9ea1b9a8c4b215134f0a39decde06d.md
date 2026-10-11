For the most part, SAP was a joy for network administrators because little or no manual configuration was involved. Everything just worked. There are, however, two problems associated with this implementation. First, SAP can become a bandwidth hog. Referring to Figure 5.2, imagine what would happen if there were hundreds of servers and thousands of clients on the network. Every service advertises its availability regardless of whether anyone wants to use it. A large portion of your network bandwidth can be used up by traffic that isn't necessary.

The second problem is that SAP is dependent on IPX. When Novell rewrote eDirectory to run on TCP/IP hosts, it had to come up with a new way for services to be located. Novell could have used static methods such as the hosts file or an option delivered via DHCP. Novell system administrators had become quite used to the automated nature of SAP. Using the hosts file would require a tremendous amount of manual configuration. Using a DHCP option is a little better; however, it doesn't carry any state information. In other words, it delivers the service address regardless of whether the service is up or down.

To keep directory services working the way they had under IPX, Novell worked with several other industry vendors to author RFC 2165 and RFC 2608, which define the Service Location Protocol (SLP).

SLP provides a level of automation on a TCP/IP network similar to that provided by SAP on an IPX network. It also eliminates some of the problems associated with SAP. Because of the way SAP broadcasts service availability, it is usually categorized as a *push* protocol, whereas SLP is categorized as a *pull* protocol.

Let's take a closer look at how SLP provides network service discovery without using large amounts of bandwidth the way SAP does.

# ## How SLP Works

SLP uses software agents that run on both the network servers and on the workstations. When an SLP-aware service is brought up, it registers itself with an agent on a server. When a host needs to locate a service, its agent sends out a request with a description of the service. Agents that have the requested information respond to the request with the necessary information. This process is shown in Figure 5.3.

SLP responses are sent in the form of a URL, though. The format of the URL is slightly different from the URLs you use in a web browser. The general format of the URLs is as follows:

*service*:*service_name*://*service_address_or_hostname*
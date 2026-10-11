# CONFIGURING SERVER PROPERTIES

You access the DNS server properties sheets to configure the various DNS functions that you want your server to perform.

Depending on the needs of your network, you may want to restrict a DNS server so that it only listens for query requests on certain IP addresses. This feature allows you to use a DNS server for a specific group of clients. You can enable this option, or simply allow the DNS server to listen on all IP addresses on the Interfaces tab.

The Forwarders tab enables you to configure *forwarders*—which is a DNS service that is configured to provide recursive service for other DNS servers. The forwarder helps other DNS servers resolve a DNS name request that cannot be resolved by forwarding the request to other DNS servers. If your server is the root DNS server, the forwarders option is not available because it is the root server.

![](bbox=[0.03, 0.51, 0.46, 0.84])

+   1. Select the desired server in the console.

![](bbox=[0.5, 0.51, 0.96, 0.84])

+   2. Click *Action*→*Properties*.
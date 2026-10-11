# FIGURE 5.3
Finding services with SLP.

![](bbox=[0.28, 0.09, 0.83, 0.28])

Here are sample URLs associated with the eDirectory service:

+   - **LDAP server** — service:ldap://192.168.1.100:389
+   - **eDirectory tree** — service:NDAP:novell://CLE-TREE.

SLP doesn't use the networkwide service-announcement broadcasts that SAP uses. Service information is only sent when it is requested. In addition, the requested information is sent only to the host that requested it. By implementing SLP in this way, Novell effectively reduced the high bandwidth usage associated with SAP.

Let's talk about the different types of agents used by SLP.

# SLP Agents

The three types of SLP agents are detailed in the following list:

+   - **User Agent (UA)** — UAs are used by applications or services to locate services on the network. UAs query Service Agents or Directory Agents to retrieve URLs containing information about the requested service. UAs are always implemented and automatically start when the SLP service is started.

+   - **Service Agent (SA)** — SAs are run on service providers (servers). As with UAs, SAs are always implemented and are automatically run when the SLP service is started. When an SLP-aware application or service is run on the server, it registers itself with the SA. The SA keeps a list of all currently available services on the local server. If a service is shut down, it “deregisters” itself with the SA. By doing this, the SA keeps a dynamic database of services. The SA listens for requests from UAs. If the SA has a record for the service a particular UA is requesting, it responds with the service name and address. SAs can also be configured to register their services with a Directory Agent.

+   - **Directory Agent (DA)** — DAs are centralized storehouses for service information on a network. By default, DAs are not automatically
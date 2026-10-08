![](bbox=[0.05, 0.11, 0.56, 0.51])

# **MC/ServiceGuard**

MC/ServiceGuard is a high availability software product that detects system failures, network or LAN card failures, and the failures of critical applications. MC/ServiceGuard can be configured to handle these failures automatically. For example, a failed critical application can be restarted. The failure of a LAN card can result in the automatic configuration of a backup LAN card to take over the network load.

MC/ServiceGuard is much more than a monitoring product, because it also provides transparent application restart when failures are detected. If you are responsible for monitoring a network, and MC/ServiceGuard is being used in your environment, then you should become familiar with how the MC/ServiceGuard product uses the network.

Although MC/ServiceGuard can be used for a single system to provide transparent LAN failover, it is more commonly used in a cluster environment. In this case, if a system failure occurs, an application can be restarted on another system. This capability requires MC/Service-Guard to be sending packets over the network, to ensure that its cluster members are still alive. You may want to have a dedicated network for this high availability communication, to ensure that high network utilization doesn't cause an unnecessary migration of your application. MC/ServiceGuard monitors subnetworks and can send an SNMP trap when a subnetwork goes
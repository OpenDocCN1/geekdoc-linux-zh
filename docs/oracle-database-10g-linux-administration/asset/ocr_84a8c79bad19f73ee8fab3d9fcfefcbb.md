The Automatic Workload Repository tracks service-level statistics as metrics. Server-generated alerts will be sent out when they exceed or fall below certain thresholds. The DBA has the option to then respond by stopping overloaded processes, changing the priority of a job, or by modifying a service-level requirement. This enables the DBA to maintain continued service availability despite service-level violations.

You can configure

+   * Priorities relative to other services
+   * The measurement of service quality
+   * Alert mechanisms and event notification to monitor changes to service quality
+   * Recovery scenarios for responses to service quality changes

The Automatic Workload Repository ensures that the CRS workload management framework and resource manager have persistent and global representations of performance data. Such information helps Oracle schedule job classes by service and to assign priorities to consumer groups. If necessary, you can rebalance workloads manually with a PL/SQL procedure. You can use this procedure to disconnect sessions but leave the service running.

When an instance goes offline due to a failure, CRS will relocate the service to another available instance. CRS relocates the service and reestablishes the connection without service interruption. The underlying service components on which the relocation relies must be enabled for relocation and restarted. Otherwise, the connections cannot be reestablished.

# VIP: Virtual Internet Protocol

One of the new features of Oracle 10g RAC is the Virtual Internet Protocol, or VIP. This is a virtual IP address that is used for failover of the nodes in the cluster.

Let’s go back and review the requirements for Oracle 9i RAC IP addresses. RAC used two addresses: one for the private interconnect network and one for the public network external to the cluster. To access the RAC database, you must specify the public IP addresses/hostnames in the tnsnames.ora file.

With 10g RAC, there is now a requirement for three IP addresses for each node in the cluster. The additional IP is for the virtual IP (VIP). You can now use the VIP in the tnsnames.ora file in place of the public IP. The VIP will fail over to a surviving node if a failure is detected.

Both the VIP and the public IP need to be defined in the DNS. The VIP is configured using the VIPCA (Virtual Internet Protocol Configuration Assistant) utility, which is invoked during the Oracle CRS installation procedure.
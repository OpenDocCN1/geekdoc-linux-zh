# Determining Network Bottlenecks

A network bottleneck is a point in the path between two networked hosts at which the available bandwidth is considerably limited. Bottlenecks can often cause serious network performance degradation problems. A bottleneck can be caused by a variety of different factors, including network misconfigurations, hardware errors, and overworked servers. Traffic analyzers are valuable tools for detecting network bottlenecks because they allow traffic flow statistics to be viewed and analyzed for anomalies.

The ntop traffic analyzer is a useful tool for detecting network bottlenecks, since it makes a variety of statistical traffic flow information available to the administrator through an easy-to-use interface. It also makes tracking down the source of network bottlenecks an easier task, through the use of data flow filtering expressions. These allow statistics to be gathered for flows of packet data matching a specific user-defined filtering criteria.

When attempting to detect network bottlenecks, the ntop tool is most useful when executed in Web mode. The ntop Web mode provides many types of network statistics information not available in interactive mode. This additional information can be helpful in the analysis of network traffic and detection of bottleneck conditions.

Table 16.4 is a listing of ntop information viewing modes that can be useful when attempting to detect network bottlenecks.

# TABLE 16.4 Ntop Traffic Views Useful for Detecting Bottlenecks

| View Name | Description |
|---|---|
| Sort Traffic by Data Received | Allows the hosts that are sending or receiving the most data to be shown. These modes can be useful when attempting to determine if a network server is being overloaded with client requests. |
| Sort Traffic by Data Sent | |
| Remote to Local IP Traffic | Displays statistics information for traffic flowing between hosts on local networks, flowing to remote networks, or flowing from remote networks. These modes can be useful when attempting to determine if a network bottleneck is located on an internal or external network. |
| Local to Remote IP Traffic | |
| Local to Local IP Traffic | |
| IP Protocol Distribution Statistics | These modes display information regarding IP protocol usage. They can be useful when attempting to determine the protocols that are utilizing the most bandwidth on a network. |
| IP Protocol Usage | |
| IP Traffic Matrix | Displays IP traffic flow information in a table format. Allows for side-by-side comparative analysis of flow statistics, so that anomalies may be detected. |
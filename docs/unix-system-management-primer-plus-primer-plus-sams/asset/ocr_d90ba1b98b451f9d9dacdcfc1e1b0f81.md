# Planning for Future Network Capacity

Network capacity is one of the most limiting factors in any technology environment, due to the large amount of infrastructure needed to implement it. For example, just a single T1 from your office to the Internet requires a physical circuit (a PRI line) from the local phone company, CSU/DSU units to translate the T1 signal, a router to connect the CSU/DSU units to your network, and an ISP to provide Internet service at the other end of the circuit.

All of this effort and its associated cost gets you 1.544Mbps of bandwidth to the Internet. If you suddenly need more, you will have to repeat this arduous process for another T1 or possibly higher bandwidth line. There are several measures you can take to make sure your organization has enough flexibility in its bandwidth solutions as well as the foresight to predict problems before they arise.

# Watch Long-Term Trends in Network Traffic

Trend analysis is an important part of system administration, and nowhere is this more obvious than in network planning. A small company with 16 employees might start out with a single T1 to the Internet for Web and email functionality, realizing that their average utilization will rarely approach the 1.544Mbps capacity of the line. The company’s usage will grow with the company, however, and eventually that same 1.544Mbps will be a bottleneck for their communications. The astute system administrator monitors the bandwidth utilization over time and therefore can predict the approximate point at which bandwidth is necessary.

Figure 11.4 shows an example of one year’s worth of bandwidth utilization on a fractional 768Mbps T1 line. Since late January, utilization has steadily increased (when read to left), but is still nowhere near the capacity of the T1 line (98Kbps). However, now that the system administrator knows that utilization is increasing, he or she can watch the graph in the next few months to see and recommend more bandwidth before the situation becomes critical. If this increase in utilization can be correlated with other factors—such as new hires—the administrator can predict bandwidth needs simply by knowing how many people are being hired.

FIGURE 11.4
An MRTG graph representing one year of bandwidth measurements on a fractional T1 line.

![](bbox=[0.315, 0.675, 0.683, 0.786])
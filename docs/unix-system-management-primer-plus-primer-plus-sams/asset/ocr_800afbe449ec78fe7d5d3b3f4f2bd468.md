# Chapter 6 • MONITORING SERVICES 143

Such network bandwidth usage "spikes" are normal, and as a system administrator, you should expect to see them periodically. However, if this kind of bandwidth usage continued over a period of time, it definitely would be a cause for concern, and may indicate one or more of the following problems:

+   - Misbehaving application Configuration mistakes might cause an application to send a flurry of network traffic to others.

+   - Denial-of-service (DoS) attack A person outside of your organization may try to disable your network services by flooding them with an excess of traffic. Chapter 13, "Implementing System Security," discusses denial-of-service attacks in more detail.

+   - Inappropriate use of network resources An employee could be downloading large files like MP3s or listening to streaming audio, which can take up significant portion of an organization's bandwidth.

+   - Inadequate bandwidth for normal operations You may not have bandwidth for all of the network services you run. You can determine bandwidth needs with tools like topdump and ntop that can help you profile your traffic. These tools are described in the "Monitoring Traffic Contents" of this chapter.

# A Fractional T1 Is Scalable

If your requirements are unknown, start small and order a fractional T1, at 512Kbps or 768Kbps, for example. If you need more bandwidth in the future, you won't have to order a new T1 and incur the costs and waiting associated the activation process—your provider can usually increase your capacity while keeping the same circuit.

One of the best and most widely used tools for recording bandwidth utilization is MRTG (Multi Router Traffic Graph), which can be downloaded from http://www.mrtg.org. You can run MRTG periodically from cron on a Unix server to query routers, and other network devices for statistics via SNMP (see Chapter 12, "Process Automation," for more information on automating tasks with cron). MRTG stores these statistics and creates daily, monthly, and yearly graphs of the data, which is extremely useful to show trends over time.

# You Can Use MRTG to Monitor Other Network Statistics

In this section, we use MRTG to graph network bandwidth over time, but it is not limited to measuring bandwidth. Any statistic available through an SNMP query can be graphed with MRTG, such as CPU usage, disk capacity, and network errors.

Figure 6.2 shows an MRTG-generated graph for a company's primary Internet connection over a T1. Note the trend: a slow buildup of traffic in the morning as employees arrive, and a slow decrease in traffic in the late afternoon as people head home for the night. You would expect this pattern to repeat itself day after day, save for weekends when nobody is at the office. Daily graphs trend to be "spiked," in that short surges in network usage show up as
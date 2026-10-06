# 32 UNIX SYSTEM MANAGEMENT PRIMER PLUS

![](bbox=[0.135, 0.073, 0.185, 0.103])

# Average Bandwidth Utilization

The average bandwidth utilization on a circuit should be no more than 30%, with peak usage not exceeding 70%. Beyond this, spikes in usage can bring a circuit dangerously close to capacity and degrade the performance of other network traffic on the line.

# Use Variable-Bandwidth Circuits

With the increasing use of fiber and other high-capacity media, many ISPs are able to offer customers variable-bandwidth solutions, even to their offices. Variable-bandwidth circuits usually offer a set bandwidth to which you agree to limit the majority of your utilization, but the circuits are not physically capped at that limit; you are allowed to "burst" up to a much higher maximum rate for short periods of time. This leeway allows for spikes in traffic; the circuits are called burstable.

Burstable bandwidth is very convenient it offers you the capacity of a high-bandwidth circuit like a DS-3 for just a little more than the cost of a lower-capacity circuit like a T1. For example, if your expected average utilization on a new T1 is less than 25%, but you occasionally need to transfer several hundred megabytes in size within 5 minutes, you should consider purchasing burstable bandwidth from your ISP Many ISPs will charge by bandwidth per interval. For example, on a burstable T1 you might be charged $1 for every 5-minute interval that your utilization exceeds 1.544Mbps.

# Summary

Performance tuning and capacity planning are two vast disciplines that go hand in hand, and every system administrator should have a basic understanding of the concepts within each of them. These complex responsibilities are much easier to manage and if you categorize them according to the four major subsystems on a server: CPU, storage, memory, and networking. To manage performance tuning and capacity planning for your network, you first understand what metrics you must compile and how to determine what they tell you about your particular operating system. With this data, you can know what to expect from the normal behavior of your systems. When abnormalities arise, you are then better to see what system components need to be tuned. You also recognize trends that can help you plan for the future. This chapter merely skimmed the surface of performance tuning and capacity planning, providing a high-level view of very complex topics; several books listed in Appendix are dedicated to these subjects and can provide more details than you will ever need.
# Working with IPS/IDS

Once the intrusion is detected, the IDS will send an alert to a security analyst for further investigation and action (as shown in the following figure):

![](bbox=[0.157, 0.153, 0.792, 0.335])

Figure 8.28 – IDS representation

In terms of deployment, an IDS can be deployed at the host level (HIDS) or network level (NIDS).

There are two main IDS engines, one that is based on signatures (examples are classic antiviruses that use a database of signature to detect malicious software), and one that is anomaly-based, which detects intrusions based on deviations from established patterns. In this latter category, there are also systems that leverage cognitive computing to enhance the recognition and identification of these patterns.

# What is an IPS?

An IPS is an active system that prevents access to your network by unauthorized users. As represented in the following figure, an IPS will automatically block any traffic that may be considered a threat to your network:

![](bbox=[0.197, 0.68, 0.753, 0.866])

Figure 8.29 – IPS representation
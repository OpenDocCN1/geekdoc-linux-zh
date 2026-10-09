![](bbox=[0.115, 0.088, 0.825, 0.478])

**Figure 29-6**. ESS Specialist Add Storage (2 of 2) panel with LUN Allocation Update

To check on the formatting status you click the **Refresh Status** button on the **Modify Volume Assignments** panel, as shown in Figure 29-7.

In the first column, under **Volume**, you will see a percentage for each volume that is being formatted. Notice that all but the last entry are 30GB LUNs. I started these earlier, and they are still formatting. When you create multiple volumes in a short period of time, you may end up with a lot of ESS activity, which is not a problem for the horsepower of the ESS. However, if one set of volumes has a lock on the disks, then the configuration submission is refused. Don't worry! This will free up in a minute or two. I get this problem mostly when I configure a lot of small LUNs in a series. Just wait a couple of minutes and try again.

This is about it for configuring new volumes in the ESS. The look and feel of these panels will change over time, especially since IBM has put out a free MES to replace all of the Windows NT ESS Master Consoles with the new Linux Master Consoles. With the new consoles, you have serial communication, as well as TCP/IP communications. With the serial link, the ESS is not dependent on the TCP/IP network to talk to the Linux Master Console.
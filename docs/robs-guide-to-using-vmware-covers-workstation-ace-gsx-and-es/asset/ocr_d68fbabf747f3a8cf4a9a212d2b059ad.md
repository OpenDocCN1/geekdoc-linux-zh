![](bbox=[0.07, 0.06, 0.88, 0.48])

Figure 28.9: Start the cluster after installation.

11. After the installation is complete, you will see a window asking you if you want to read the Readme file. The Novell Cluster Services software is started on both servers.

12. At this time, you have an up and running cluster on your servers. The Cluster Membership Monitor (CMON.NLM) will display the two servers in the cluster with the Up status.

You can use iManager (if you have SP1a), Remote Manager or ConsoleOne to manage the cluster.

Have fun with your newly built cluster!

# 28.1 Be Careful to Suspend the Cluster Nodes

The cluster nodes will continuously keep each other informed about their status. If a node is not available, it will be marked as off-line. If you suspend a cluster node, it will no longer be available to the other node(s) in the cluster.

You may think that suspending both cluster nodes at the same time is the solution. This could work if you are fast enough, but if you bring the server back on-line from the suspend mode, the resume operation could take some time. This is especially the case if you resume two servers at the same time. There is a fair chance that they will not be resumed exactly at the same time (depending on your hardware), or that your host is so busy with this operation that the guests are slow and the heartbeat between the cluster nodes gets lost.
# 18.3.4 Corporate Cluster

Since our move to Windows-based clusters, corporate interest in CTC and our computing environment has grown substantially. We installed a dedicated cluster to provide corporate clients and partners with a place to do performance testing and code development. The corporate cluster currently has the following configuration:

+   16 Dell PowerEdge 2450 servers
+   Dual-processor Pentium III 933 MHz/256 KBytes cache
+   2 GBytes RAM/node
+   27 GBytes disk (RAID 0)/node

# 18.3.5 Computational Finance Cluster

CTC director Thomas Coleman has a research group focused on computational finance both in Ithaca and in the CTC-Manhattan office in New York City. They use clusters for such activities as portfolio risk analysis. One of the tools they find useful is the Cornell Multitask Toolbox, which enables them to use Matlab for parallel computations on the cluster. The computational finance cluster is configured as follows:

+   16 Dell PowerEdge 2450 servers
+   Dual-processor Pentium III 933 MHz/256 KBytes cache
+   2 GBytes RAM/node
+   27 GBytes disk (RAID 0)/node
+   Giganel CLAN interconnect

# 18.4 Other Cluster Resources

In addition to the CTC Windows-based clusters and the dedicated clusters, we are exploring Web-based clusters and a Windows-based CAVE environment. We believe that these resources and the applications we are developing to use them will play a major role in making high-performance computing available to the masses.

# 18.4.1 Web Clusters

As mentioned earlier, we are using the CTC serial nodes as a resource pool for new Web-based computing interfaces. To date, we have two Web-based cluster applications.

The first application, **ser-loopp**, involves protein sequence prediction. The user enter a protein sequence and a e-mail address. This sequence is then submitted to Cluster CoNTroller securely via the IIS Web server. After the **ser-loopp** code has been run against the sequence, results are e-mailed to the user that submitted the
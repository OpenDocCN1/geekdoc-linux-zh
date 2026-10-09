![](bbox=[0.25, 0.09, 0.88, 0.46])

# **Figure 17-11** Information about the new system

Cacti uses SNMP to collect information from the device. If all goes well, it will report **Save Successful** and display the information about the new system near the top of the screen (Figure 17-11).

+   • Creating a graph
+   
+   Click **Create Graphs for this Host**. Cacti displays a list of queries and data sources that it can graph (Figure 17-12, next page). Put a tick in the check box at the right end of each line that holds a data source you want to create a graph for. Click **Create**. Cacti displays a message at the top of the screen that tells you which graphs it created.

+   • Adding a node to the graph tree
+   
+   Select **Management⇒Graph** Trees and click **Add** to add a node to the graph tree. Enter a name for the new node (e.g., Servers) and click **Create**.
+   
+   Now click **Add** (on the right) to add a Tree Item, select Host from the drop-down list labeled **Tree Item Type**, select the host you just added (Cacti may add **Host** for you), and click **Create**.

+   • Wait
+   
+   Take a break for 10 or 15 minutes to allow Cacti to poll the new device a few times.

+   • Displaying the graph
+   
+   Click the **Graphs** tab. The name for the new node appears in the device tree on the left side of the screen. When you click the plus sign (+) that appears to the left of the
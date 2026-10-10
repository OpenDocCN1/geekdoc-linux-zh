
### 3. From the Ntdsutil menu, key activate instance NTDS and press (Enter). You will return to the Ntdsutil menu.

### 4. Still working from the Ntdsutil menu, key authoritative restore and press (Enter).

- To restore a single object, key restore object <ObjectDN> and press (Enter).
- To restore a container and the objects it contains, key restore subtree <ContainerDN> and press (Enter).

### 5. Click Yes to perform the authoritative restore. After the authoritative restore has completed, you will see the window shown in Figure 11-11. As you can see, this indicates that a text file was created containing information about each object that was authoritatively restored, as well as listing the name of the LDF file containing any back-link information that needs to be restored.

![](img/a8ee53dbf1310726255b6fbb9f296fb2_275_0.png)

### 6. Key quit and press (Enter) twice to return to the command prompt.

### 7. If back-links need to be restored, restart the domain controller in normal mode. Open a command prompt, key ldifde -i -f <LDIF file name> -s <FQDN of the local DC> and press (Enter).

### 8. Close the command prompt window.

**PAUSE.** Restart the domain controller in normal mode if you did not do so in step 7.

You just performed an authoritative restore of one or more Active Directory objects. When the restored domain controller is online and connected to the network, normal replication synchronizes the restored domain controller with any changes from the additional domain controllers that were not overwritten by the authoritative restore. Replication also propagates the authoritatively restored objects to other domain controllers in the forest. The deleted objects that were marked as authoritative are replicated from the restored domain controller to the additional domain controllers. Because the restored objects have the same object GUID and object SID, security remains intact, and object dependencies are maintained.

## Monitoring Active Directory

> Monitoring the Active Directory service is an important part of network administration. Monitoring enables you to take a proactive approach to network management. By raising the awareness of possible network problems before they occur, you have better control over their impact.

Creating a monitoring plan can help you flag minor processes or configuration issues before they turn into something potentially catastrophic to your network. For example, monitoring the disk space use on the drive that holds the ntds.dir file and discovering that you are low on available disk space can lead you to resolve this situation before all the free space is used.

Monitoring Active Directory can provide the following benefits:

- Early alerts to potential problems
- Improved system reliability
- Fewer support calls to the helpdesk
- Improved system performance

Several important items must be considered when developing your monitoring plan. In addition, you need to know which tools are available to assist you in monitoring the Active Directory system. The next sections discuss how to collect and locate information related to Active Directory errors and warnings by using Event Viewer and System Monitor.

### Understanding Event Logs

> Windows Server 2008 uses the Windows Event Viewer to record system events, such as security, application, and directory service events. Events related to Active Directory are recorded in the Directory Service log. The Directory Service log is created when Active Directory is installed. It logs informational events such as service start and stop messages, errors, and warnings. This log should be the first place you look when you suspect a problem with Active Directory.

Figure 11-12 shows the Directory Service log on a Windows Server 2003 computer. Because Event Viewer shows logs for informational and error messages, it is important to monitor the logs for some basic events that can indicate the system’s overall health. In the Type field of any of the log files in Event Viewer, you should monitor and filter events that indicate a warning or stop error. A warning is indicated by a yellow triangle with an exclamation mark, and a stop error is indicated by a red circle with an X on it. The event details will provide additional information that pertain to possible reasons for the entry in addition to resources that can provide possible solutions. Error codes reported by the Event Viewer can also be researched in the Microsoft Knowledge Base on the Microsoft Web site.

![](img/a8ee53dbf1310726255b6fbb9f296fb2_276_0.png)

### Using the Reliability and Performance Monitor

> The Reliability and Performance Monitor is a tool located within the Administrative Tools folder. Reliability and Performance Monitor in Windows Server 2008 allows you to collect real-time information on your local computer or from a specific computer to which you have permissions. This information can be viewed in a number of different formats that include charts, graphs, and histograms. The data can be saved or printed for documentation purposes. You can also customize the parameters that you want to track and store them in an MMC snap-in so that they can be used on other computers within your network.

![](img/a8ee53dbf1310726255b6fbb9f296fb2_277_0.png)

Before you can effectively use the Reliability and Performance Monitor shown in Figure 11-13, you need to understand how to configure it so that you can obtain the desired information. The Reliability and Performance Monitor uses categories to organize the items that can be monitored. These categories are referred to as performance objects. Performance objects contain performance counters associated with the category that you want to monitor. Performance counters are the specific processes or events that you want to track. For example, within the NTDS performance object, the Directory Replication (DRA) Inbound Bytes Compressed counter will monitor the size of compressed data that was replicated from other sites.

![](img/a8ee53dbf1310726255b6fbb9f296fb2_277_1.png)

**Figure 11-13**
Viewing the Reliability and Performance Monitor

The DirectoryServices performance object contains over 120 performance counters that pertain to Active Directory. It is important for you to determine which of these counters suit your purposes. Table 11-1 provides a breakdown of some representative counters that you should consider adding to your basic monitoring plan.

| COUNTER | DESCRIPTION |
| --- | --- |
| DRA Inbound Bytes Compressed (Between Sites, After Compression)/Sec | The compressed size, in bytes, of inbound compressed replication data. This is the size, after compression, from Directory System Agents (DSAs) in other sites. |
| DRA Inbound Bytes Compressed (Between Sites, Before Compression)/Sec | The original size, in bytes, of inbound compressed replication data. This is the size, before compression, from DSAs in other sites. |
| DRA Inbound Bytes Not Compressed (Within Site)/Sec | The number of bytes received through inbound replication that were not compressed at the source from other DSAs in the same site. |
| DRA Inbound Bytes Total/Sec | The total number of bytes received through replication per second. It is the sum of the number of uncompressed bytes and the number of compressed bytes. |
| DRA Inbound Full Sync Objects Remaining | The number of objects remaining until the full synchronization process is completed or set. |
| DRA Inbound Objects/Sec | The number of objects received, per second, from replication partners through inbound replication. |
| DRA Inbound Objects Applied/ Sec | The rate per second at which replication updates are received from replication partners and applied by the local directory service. This count excludes changes that are received but not applied, such as when the change is already present. This indicates how much replication update activity is occurring on the server due to changes generated on other servers. |
| DRA Inbound Object Updates Remaining in Packet | The number of object updates received in the current directory replication update packet that have not been applied to the local server. This tells you when the monitored server is receiving changes and taking a long time applying them to the database. |
| DRA Outbound Bytes Compressed (Between Sites, After Compression)/Sec | The compressed size, in bytes, of outbound compressed replication data, after compression, from DSAs in other sites. |
| DRA Outbound Bytes Compressed (Between Sites, Before Compression)/Sec | The original size, in bytes, of outbound compressed replication data, before compression, from DSAs in other sites. |
| DRA Outbound Bytes Not Compressed (Within Site)/Sec | The number of bytes replicated that were not compressed from DSAs in the same site. |
| DRA Outbound Bytes Total/Sec | The total number of bytes replicated per second. This is the sum of the number of uncompressed bytes and the number of compressed bytes. |
| DRA Pending Replication Synchronizations | The number of directory synchronizations that are queued for this server but not yet processed. This helps in determining replication backlog. A larger number indicates a larger backlog. |
| DRA Sync Requests Made | The number of synchronization requests made to replication partners. |
| DS Directory Reads/Sec | The number of directory reads per second. |
| DS Directory Writes/Sec | The number of directory writes per second. |
| DS Search Suboperations/Sec | Number of search suboperations per second. One search operation is made up of many suboperations. A suboperation corresponds roughly to an object the search causes the DS to consider. |
| LDAP Client Sessions | The number of connected LDAP client sessions. |
| LDAP Searches/Sec | The number of search operations per second performed by LDAP clients. |
| NTLM Binds/Sec | The number of Windows NT LAN Manager (NTLM) authentications per second serviced by this domain controller. |

**Table 11-1**
Representative NTDS Performance Object Counters

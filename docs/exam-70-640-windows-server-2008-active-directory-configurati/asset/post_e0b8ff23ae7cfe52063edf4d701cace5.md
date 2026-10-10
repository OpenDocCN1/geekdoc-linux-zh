
3. Select the site links you wish to bridge and click **Add.** Key a description for the bridge and click **OK** to finish.

**PAUSE. LEAVE** the Sites and Services MMC snap-in open to complete the next exercise.

In the previous exercise, you created a manual site link bridge for a network in which automatic site link bridging has been disabled. This is a necessary step for a company that has a physical network that is not fully routed or in situations where you wish to exert more granular control over the path taken by Active Directory replication traffic.

## Managing Replication

When monitoring Active Directory replication, any errors that occur will be logged to the Directory Services Event Viewer on each domain controller. For example, when simultaneous changes are made to an object's attributes from different domain controllers and the change cannot be updated due to a collision, the error is logged to the Event Viewer. Some of these errors may be for informational purposes, whereas others may warrant some investigation and corrective action. This section describes some of the methods used to determine which domain controllers contribute to the problems.

In many cases, after an Active Directory problem is isolated, it is necessary to initiate a forced replication to help get Active Directory up to date and consistent. Refreshing the replication topology is accomplished by forcing the KCC to run. Depending on whether you wish to refresh the intrasite topology or the intersite topology, the steps are slightly different. Refreshing the topology within a site requires the KCC to be triggered on one of the domain controllers within the site.

### REFRESH THE INTRASITE REPLICATION TOPOLOGY

**GET READY.** Before you begin these steps, log on to the console of a domain controller or an administrative workstation that has the Active Directory Administrative Tools installed.

- 1. In Active Directory Sites and Services, expand **Sites**, followed by the site where you wish to run the KCC.
- 2. Expand **Servers**, and double-click one of the domain controllers.
- 3. In the details pane, right-click **NTDS Settings**, click **All Tasks**, and select **Check Replication Topology**.

**PAUSE. LEAVE** the MMC console open to use in the next exercise.

To refresh the intersite replication topology, follow the steps listed in the previous exercise on the domain controller that has been designated as the ISTG for a particular site.

### DETERMINE WHICH SERVER HOLDS THE ISTG ROLE

**GET READY.** Before you begin these steps, log on to the console of a domain controller or an administrative workstation that has the Active Directory Administrative Tools installed.

- 1. In Active Directory Sites and Services, expand the **Sites** folder, and then expand the appropriate site.
- 2. In the Details pane, right-click **NTDS Site Settings**, and then select **Properties**. The Properties page displays the server holding the ISTG role.
- 3. To force the KCC to regenerate the intersite topology, right-click **NTDS Settings**, click **All Tasks**, and then select **Check Replication Topology**.

**PAUSE. LEAVE** the MMC console open to use in the next exercise.

The ISTG role is held by one domain controller at each site. The ISTG is designated automatically, and it is responsible for the intersite topology and the designation of bridgehead servers if you have not defined them manually. Determining which server is running the ISTG service allows you to force the KCC to run so that you can refresh the intersite replication topology.

### TRIGGERING MANUAL REPLICATION

When troubleshooting Active Directory replication, you may wish to manually force replication between two DCs in an attempt to correct any inconsistencies or errors that you have found. You may also wish to force replication to occur when you make changes, such as disabling user accounts, that you wish to replicate immediately throughout the enterprise without waiting for the next replication interval.

### FORCE MANUAL REPLICATION

**GET READY.** Before you begin these steps, log on to the console of a domain controller or an administrative workstation that has the Active Directory Administrative Tools installed.

- 1. In **Active Directory Sites and Services**, expand *Sites*, followed by the site that contains the connection for which you wish to force replication.
- 2. Locate the server in the *Servers* container that provides the connection object.
- 3. Click **NTDS Settings** in the console tree.
- 4. In the details pane, right-click the connection for which you want replication to occur and select **Replicate Now**.

**PAUSE.** Leave the MMC console open to use in the next exercise.

In the previous exercise, you used the Active Directory Sites and Services MMC snap-in to force Active Directory replication to occur. You can also perform this task using the repadmin command-line tool, which we will discuss in the following section.

## Monitoring Replication

Monitoring replication is a vital part of managing your Active Directory network because many Active Directory issues can be prevented by monitoring replication activity on your network. Windows Server 2008 provides a number of tools that allow problem discovery, diagnosis, and resolution. In addition to the directory service event log available in the Event Viewer, Windows Server 2008 provides several additional monitoring tools that are installed when you add the Active Directory Domain Services role to a 2008 server. The tools discussed here were formerly part of the Support Tools available on the Windows Server 2003 CD, but are now supported natively within the Windows Server 2008 operating system.

The monitoring tools that you will focus on here are dcdiag and repladmin, both of which can be run from the command-line of the domain controller as well as remotely from an administrative workstation.

*Dcdiag* is a command-line tool used for monitoring Active Directory. When run from a command prompt, this tool can do the following:

- Perform connectivity and replication tests, reporting errors that occur
- Report DNS registration problems
- Analyze the permissions required for replication
- Analyze the state of domain controllers within the forest

To view all of the options and syntax for dcdiag, use the /? option from a command prompt as follows:

`dcdiag /?`

An example of the syntax required to check replication connections using dcdiag is as follows:

`dcdiag /test:replications`

Repladmin is a command-line tool used for the following:

- To view the replication topology from the perspective of each domain controller. This aids in understanding how information is transferred, ultimately assisting in the isolation of replication problems.
- To manually create a replication topology if site link bridging is disabled because the network is not fully routed.
- To force replication between domain controllers when you need updates to occur immediately without waiting for the next replication cycle.
- To view the replication metadata, which is the combination of the actual data and the up-to-date vector or USN information. This is helpful in determining the most up-to-date information prior to seizing an operations master role.

Like dcdiag, you can view a complete list of syntax options for repladmin by using the /? switch. The following example illustrates this:

`repladmin /?`

The following is an example of the syntax to show all replication partners for server1 in the cohowinery.com domain:

`repladmin /showreps server1.cohowinery.com`

## SUMMARY SKILL MATRIX

**IN THIS LESSON YOU LEARNED:**

- To define and manage sites and site links.
- To determine a site strategy based on the physical network infrastructure.
- To use Active Directory Sites and Services to configure replication.
- To understand the differences between intrasite and intersite replication.
- To describe the role of the Intersite Topology Generator (ISTG) and Knowledge Consistency Checker (KCC) in site replication.
- To optimize replication by configuring bridgehead servers and site link bridging.
- To monitor replication using dcdiag and repladmin.

## Knowledge Assessment

### Fill in the Blank

*Complete the following sentences by writing the correct word or words in the blanks provided.*

1. The amount of time that it takes for a change to be replicated to all domain controllers in an environment is called ____________.
2. The default ____________ of any new site link is 100.

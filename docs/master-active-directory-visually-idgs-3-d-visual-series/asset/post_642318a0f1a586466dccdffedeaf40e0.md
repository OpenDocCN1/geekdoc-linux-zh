
## MANAGING DOMAIN CONTROLLERS (CONTINUED)

The Operating System tab tells you the operating system, version number, and the service pack that has been applied (if any). As service packs are released for Windows 2000 and applied to the domain controller, the service pack version number appears in this tab. This is an easy way to track your domain controllers and make certain that they all have the most current service pack applied.

The Member Of tab tells you which groups the server belongs to. As with users, a computer account can belong to different groups. Use the Member Of tab to manage the groups to which the domain controller belongs. By using the Add and Remove buttons, you can easily manage the group membership of the domain controller and change them when necessary.

The Location tab tells you which locations are served by the site in the directory. If you have multiple sites, you can click the Browse button to choose additional locations.

![](img/763d5ae436311371600c0952a3da9094_355_0.png)

![](img/763d5ae436311371600c0952a3da9094_355_1.png)

- 3 Click the Operating System tab.
  - This tab tells you what operating system, version number, and service pack (if any) is in use for the server.
- 4 Click the Member Of tab.
  - The Member Of tab tells you what groups the server is currently a member of.
- 5 To add the server to more groups, click Add.
- 6 Select the group you want to add the server to.
- 7 Click Add.
- 8 Repeat Steps 6 and 7 to add the server to more groups.
- 9 Click OK when you are done.
- 10 Click the Location tab.
  - This tab tells you which locations are served by the site in the directory.
- 11 Click Browse to choose a different location.

### To how many groups should a domain controller belong?

You can allow the domain controller to be a member of any group you choose. However, for administrative purposes, you should limit group membership to those that are necessary. Excessive group memberships may cause permission problems. See Chapter 14 for more information about group accounts.

### If I use the Remove button to take a group membership away from a server, will this affect the other groups?

No. Each group functions on its own, so you can add and remove group membership for the server without affecting other groups. The server should, however, remain in any default groups configured by Windows 2000 (such as the Domain Controllers group). Keep in mind that computer group membership functions in much the same way as user group membership. The purpose is to organize computer accounts so they can access desired resources and have rights applied for the desired groups.

![](img/763d5ae436311371600c0952a3da9094_356_0.png)

![](img/763d5ae436311371600c0952a3da9094_356_1.png)

On the Managed By tab, you can assign a manager for the domain controller. After you configure a manager for the domain controller, the manager's name and contact information is taken from the Active Directory and automatically entered on the Managed By tab. This feature enables you to easily see who manages various domain controllers and how to contact the manager. Of course, this information is not required on this tab and does not appear if the contact information is not configured in the manager's Active Directory user account.

You can also see more information about the manager by clicking the View button. This action opens the properties sheet for the user or group from the Active Directory who manages the domain controller. If no additional information is configured in the manager's user account, then it will not be viewable.

![](img/763d5ae436311371600c0952a3da9094_357_0.png)

- 12 Click the Managed By tab.
- 13 To add a manager for the server, click Change.
- 14 Select the user account or group account you want to designate as the manager.
- 15 Click OK.
- 16 The new manager's name and contact information — taken from the Active Directory — now appears.
- 17 To view additional Active Directory information about the manager, click View.
  - The Properties sheet for the manager appears.
- 17 Click OK when you are done.

### TIPS

### How can I keep a manager's contact information private?

A manager's contact information is taken from the information configured in the manager's Active Directory user account. In order to keep the contact information (such as the manager's phone number) private, you have to delete this information from the manager's user account in the Active Directory. By doing so, no Active Directory users can read the information because it does not appear in the manager's account.

### Do I have to assign a manager?

No. You are not required to assign a manager on this tab. In some cases, a single person or group manages all domain controllers, in which case, you do not need to assign a manager using the Managed By tab. This is strictly an administrative issue and not a required configuration component of the Active Directory.

![](img/763d5ae436311371600c0952a3da9094_358_0.png)

![](img/763d5ae436311371600c0952a3da9094_358_1.png)

## SECTION VI

### 19) ACTIVE DIRECTORY REPLICATION CONCEPTS

- What Is Replication? ...338
- Understanding Replication Topology ...339
- How Replication Works in the Active Directory ...340
- Understanding Replication Partitions ...346

### 20) USING THE ACTIVE DIRECTORY DOMAINS AND TRUSTS CONSOLE

- Connecting to a Domain Controller ...348
- Changing the Operations Master ...350
- Creating UPN Suffixes ...352

### 21) MANAGING DOMAINS AND TRUSTS

- Managing Domain Controllers ...354
- Accessing Domain Properties ...356
- Changing the Domain Mode ...358
- Configuring Trusts ...360
- Assigning a Domain Manager ...362

![](img/763d5ae436311371600c0952a3da9094_360_0.png)

**Connected Users**

| User | Resources In Use |
| :--- | :--- |
| MSmith | Anderson Account |
| GBlack | Sales Info |
| GBlack | (printer icon) |
| SJones | (printer icon) |
| SJones | 1998 Budget |

**Server Manager**

### WHAT IS REPLICATION?

Replication is the process of sending update notifications to other Active Directory domain controllers when changes or updates occur in the Active Directory. Imagine you have two documents that are exactly alike. If you change a sentence in one document, you must also change the same sentence in the second document to keep them exactly the same.

The purpose of replication is the same—to *replicate*, or copy, changes to other Active Directory databases so that all Active Directory data on all domain controllers is exactly the same. Through Active Directory replication, all domain controllers are assured of having correct database information that accurately reflects the resources available in the Active Directory environment.

![](img/763d5ae436311371600c0952a3da9094_361_0.png)

![](img/763d5ae436311371600c0952a3da9094_361_1.png)

![](img/763d5ae436311371600c0952a3da9094_361_2.png)

![](img/763d5ae436311371600c0952a3da9094_361_3.png)

Changes made on one Active Directory domain controller are replicated to all other Active Directory controllers so that all domain controllers have exactly the same information.

### UNDERSTANDING REPLICATION TOPOLOGY

Active Directory replication occurs between two topologies—Intrasite and intersite. Intrasite replication occurs within a site, which is a grouping of computers or domains connected by high-speed bandwidth. (You can learn more about sites in Chapters 22 and 23.) Within a site, or intrasite, the Active Directory automatically generates a replication topology; it determines how the domain controllers replicate data to one another. This feature is a great administrative benefit because it removes the burden of manually configuring replication between domain controllers.

For intersite replication, you manually establish the site link used to replicate data (see Chapter 23). Sites are generally connected by slower or less reliable links, and a replication topology is not automatically generated between sites.

In order to fully understand the replication process, you should understand how the Active Directory automatically generates the intrasite replication topology. Replication topology defines the pathways between domain controllers through connection objects and the Knowledge Consistency Checker (KCC).

Replication occurs through domain controller partners. The Active Directory determines whether a domain controller is a direct partner with another domain controller or if it receives replication indirectly from a domain controller through transitive replication. This simply means that if Server1 is a direct partner with Server2, and Server2 is a direct partner with Server3, then Server3 receives replication data indirectly (transitively) from Server1. The KCC determines how domain controllers are partnered so that all domain controllers receive replication data. Direct connections are called connection objects and are unidirectional between the two domain controllers. In other words, a potential direct partner domain controller is seen as a connection object in terms of the replication topology. The Active Directory automatically generates connection objects based on information about the sites, subnets within the sites, and cost of connections. The KCC uses this information to generate a replication topology in a bi-directional ring (by default). When a change is made to the Active Directory that needs to be replicated, the replication engine on the domain controller begins the replication process at a defined interval when replication can occur (every five minutes by default). Then, it notifies its first replication partner, which notifies its partner, and so forth. By this design of direct and indirect replication, replication within a site generally takes about 15 minutes to replicate to all domain controllers.

![](img/763d5ae436311371600c0952a3da9094_362_0.png)

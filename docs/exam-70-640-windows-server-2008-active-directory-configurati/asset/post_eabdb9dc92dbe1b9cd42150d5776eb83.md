
**4.** Select the Enable Universal Group Membership Caching checkbox, as shown in Figure 4-1.

![](img/a8ee53dbf1310726255b6fbb9f296fb2_124_0.png)

**Figure 4-1**  
Enabling universal group membership caching

**5.** In the Refresh Cache From field, select a site that you wish this site to receive updates from or leave it at `<Default>` to refresh from the nearest site that contains a global catalog server. Click **OK**.

**PAUSE.** CLOSE the Active Directory Sites and Services MMC snap-in.

You have just enabled universal group membership caching for a single site within Active Directory. This setting must be enabled for each site that you wish to configure for universal group membership caching.

## Configuring Additional Global Catalog Servers

> By default, the first domain controller in a forest is a global catalog server. Therefore, your initial site will already contain a global catalog server.

The following guidelines will help you decide when you should add a global catalog server.

- Each site should contain a global catalog server to facilitate user logons. If a remote site is located across an unreliable or slow WAN link, a locally deployed global catalog server will allow logons and Active Directory searches to take place regardless of the state of the WAN link. If this is not possible, consider enabling universal group membership caching.
- When placing a global catalog at a remote site, consider the amount of bandwidth necessary to replicate global catalog information. Responding to logon requests from other sites increases the demands on bandwidth for the remote site.
- The domain controller that hosts the global catalog must have enough space on the hard drive to house the global catalog. As a rule of thumb, you should estimate 50 percent of the size of the `ntds.dit` file of every other domain in the forest when sizing hardware for a global catalog server.
- A site that contains an application using port 3268 for global catalog queries should contain a global catalog server. Port 3268 is used for Active Directory object searches.

## CONFIGURE AN ADDITIONAL GLOBAL CATALOG SERVER

**GET READY.** Before you begin these steps, you must be logged on as a member of the Domain Admins group.

**1.** On the domain controller where you want the new global catalog, open **Active Directory Sites and Services** from the Administrative Tools folder.

> **CERTIFICATION READY?**  
> Configure the global catalog  
> 2, 5

**2.** In the console tree, double-click **Sites**, and then double-click the site name that contains the domain controller for which you wish to add the global catalog.  
**3.** Double-click the **Servers** folder and select your domain controller. Right-click **NTDS Settings** and select **Properties**.  
**4.** On the **General** tab, select the **Global Catalog** checkbox, as shown in **Figure 4-2**, to assign the role of global catalog to this server. Click **OK**.

![](img/a8ee53dbf1310726255b6fbb9f296fb2_125_0.png)

![](img/a8ee53dbf1310726255b6fbb9f296fb2_125_1.png)

**PAUSE.** **CLOSE** the Active Directory Sites and Services MMC snap-in.

> **TAKE NOTE**  
> You also have the option to configure an RODC to host the Global Catalog Server role.

You have just configured a domain controller as an additional global catalog within an Active Directory domain. You can enable some or all domain controllers in a forest as additional global catalog servers in your environment. You will need to allow sufficient time for the account and schema information to replicate to the new global catalog server. The length of time this process takes will vary depending on the number of objects to be replicated and the speed of the link used for the transfer. The **Directory Services Event Viewer** will display **Event ID 1119** when the computer is ready to advertise itself as a global catalog server.

## Understanding Flexible Single Master Operations (FSMO) Roles

As discussed previously, Active Directory is a multimaster database, which means that updates to the Active Directory database can be made by any writable domain controller in your environment. However, some sensitive operations need to be controlled more stringently than others, such as schema management and adding or removing additional domains from an Active Directory forest. These specialized roles are called **Flexible Single Master Operations (FSMO)** roles. Beyond acting as a normal domain controller in the replica ring, the domain controllers that hold these FSMO roles are responsible for providing services classified as single-master operations. This means only one domain controller in each domain or, in some cases, one domain controller in each forest can provide a particular operation. By employing single-master operations servers, you can more closely control the kinds of operations that might create issues in Active Directory if more than one domain controller were able to perform them at one time.

> **THE BOTTOM LINE**

As you have already learned, writable Active Directory domain controllers follow a multi-master replication model. This multimaster model ensures that multiple copies of all domain objects provide ease of accessibility and fault tolerance. In addition, any domain controller can update the contents of the database when changes occur. This multimaster model provides a fast and efficient directory service when the implementation guidelines are followed.

Although Active Directory has mechanisms, such as version IDs and timestamps, to assist in possible conflict resolution, critical functions need to have the assurance of little or no risk of errors. An example of a task that should not be subject to more than one simultaneous change is illustrated in the following scenario.

You are the network administrator for Margie's Travel. Your company has seven locations scattered throughout the world. As part of the application deployment team, you are assigned the job of installing a newly developed application on the network. Part of the instructions for the installation requires that you add a custom attribute to several objects in Active Directory. Unknown to you or your manager, another administrator at a different location has been assigned the same task. You and the other administrator are working on the task at the same time.

Assuming you are attempting to do the tasks simultaneously on a multimaster platform, you could end up with a corrupted Active Directory schema due to conflicting simultaneous changes. However, in Server 2008, Active Directory this type of situation will not occur because Microsoft has implemented FSMO roles to avoid this type of corruption. These roles are performed by only one specific server, which eliminates the risk associated with database corruption due to these kinds of sensitive tasks.

Active Directory supports five FSMO roles. Their functionality is divided between domain-wide and forest-wide FSMOs. In a small-business scenario, where there may be only one domain and a single domain controller, all of the roles can exist on the same domain controller. If you deploy a second domain controller for fault tolerance, you can *transfer* some of these FSMO roles to the new domain controller. This offers not only fault tolerance, but also performance improvements because processing these tasks is balanced between more than one server.

Three roles are domain specific:

- **Relative Identifier (RID) Master.** Responsible for assigning relative identifiers to domain controllers in the domain. Relative identifiers are variable-length numbers assigned by a domain controller when a new object is created.
- **Infrastructure Master.** Responsible for reference updates from its domain objects to other domains. This assists in tracking which domains own which objects.
- **Primary Domain Controller (PDC) Emulator.** Provides backward compatibility with Microsoft Windows NT 4.0 domains and other down-level clients. Password changes, account lockouts, and time synchronization for the domain will also be managed by the PDC Emulator. The domain controller that initiates a password change will send the change to the PDC Emulator, which in turn updates the global catalog server and provides immediate replication to other domain controllers in the domain.

Let's examine these three FSMO roles in more detail.

The domain controller that is assigned the RID Master role in a domain is responsible for generating a pool of identifiers that are used when new accounts, groups, and computers are created. These identifiers are called *relative identifiers* (RID) because they are related to the domain in which they are created. The RID is a variable-length number that is assigned to objects at creation and becomes part of the object's *security identifier* (SID). A SID is used to uniquely identify an object throughout the Active Directory domain. Part of the SID identifies the domain to which the object belongs, and the other part is the RID.

Each domain can have only one RID Master. When two or more domain controllers exist in a domain, the RID Master assigns a block of 500 identifiers to each domain controller. When

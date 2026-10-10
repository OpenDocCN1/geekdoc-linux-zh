
## Fill in the Blank

- 3. Intersite replication uses `__________` traffic to reduce the impact to bandwidth on corporate WAN links.
- 4. The KCC creates a(n) `__________` to allow replication to take place in the opposite direction in the event that a single domain controller in the replication topology fails.
- 5. The purpose of the KCC is to create a(n) `__________` between multiple domain controllers within a site as well as between sites.
- 6. By default, all Active Directory site links are `__________`.
- 7. When Active Directory detects a replication conflict in which two objects have been modified nearly simultaneously, the first attribute that Active Directory will use as a tie-breaker is the `__________`.
- 8. Active Directory will designate a(n) `__________` within each site to manage intersite replication activity.
- 9. The minimum `__________` that you can assign to a site link is 15 minutes.
- 10. Within a single site, domain controllers will use `__________` to inform other DCs that intrasite replication needs to take place.

## Multiple Choice

Circle the correct choice.

- 1. The KCC is responsible for calculating intrasite replication partners. During this process, what is the maximum number of hops that the KCC will allow between domain controllers?
  - a. 2
  - b. 3
  - c. 4
  - d. 5

- 2. Replication that occurs between sites is called `__________` replication.
  - a. Local
  - b. Remote
  - c. intersite
  - d. Intrasite

- 3. Company XYZ is a national company with locations in Detroit, Minneapolis, Phoenix, and Dallas. There are two connections between Detroit and Minneapolis. The first is a T-1 link and the second is a 128-Kbps link. When setting up the site links for replication, what should you do to ensure that the 128-Kbps link is used only if the T-1 is unavailable?
  - a. Set a cost of 1 for the T-1 and a cost of 5 for the 128-Kbps link.
  - b. Set a cost of 5 for the T-1 and 1 for the 128-Kbps link.
  - c. Leave the costs at their default value of 100.
  - d. Change the schedule manually to disallow replication on the 128-Kbps link until it is needed.

- 4. You are the administrator for a network that has several sites. There is a site link from the main headquarters to each remote site for file transfer and replication purposes. You have been asked to create five new users on the network, and several of the users need immediate access to network applications. When asked by your manager how long replication of these new accounts will take, what is your response?
  - a. Replication occurs every 180 minutes by default.
  - b. Replication occurs at 15-minute intervals.
  - c. Replication occurs as soon as the account is added.
  - d. Replication occurs only between 12:00 AM and 6:00 AM.

- 5. Given the scenario in question 4, how long would it take for other DCs within the headquarters site to replicate the accounts belonging to the new users?
  - a. Replication occurs every 180 minutes by default.
  - b. Replication occurs at 15-minute intervals.
  - c. Replication occurs within 15 seconds of the account being added.
  - d. Replication occurs only between 12:00 AM and 6:00 AM.

- 6. What mechanism is used by an Active Directory domain controller to indicate that it has unreplcated changes to communicate to its replication partners?
  - a. Preferred bridgehead servers
  - b. Change notification
  - c. Site link bridges
  - d. intersite replication

- 7. When would you disable automatic site link bridging within Active Directory Sites and Services?
  - a. When you need to configure intersite replication
  - b. When you wish to configure different costs for your site links
  - c. When your physical network is not fully routed
  - d. When you wish to control the hours during which intersite replication will occur

- 8. To optimize client authentication and location of resources, which kind of object should each Active Directory site contain?
  - a. Site links
  - b. Costs
  - c. Connection objects
  - d. Subnets

- 9. Which of the following naming contexts are replicated across an entire Active Directory forest?
  - a. Configuration and Schema
  - b. Schema and DomainDNSZones
  - c. Configuration and ForestDNSZones
  - d. Schema and ForestDNSZones

- 10. When creating a site link, you can configure it to use which of the following protocols?
  - a. TCP/IP or RPC over IP
  - b. RPC over IP or SMTP
  - c. SMTP or TCP/IP
  - d. SMTP or CIDR

## Case Scenarios

### Scenario 3-1: Adding a New Site to a Network

Your company is located in the United States, and it has just added a location in Canada that will need to become part of your Active Directory network. Your network designer has provided you with the following configuration information regarding the new location servers and the connections that have been procured.

Three new servers will be installed in the Canada facility with the following specifications:

- Server 1: 2.4-GHz processor with 2 GB RAM will be installed as a domain controller.
- Server 2: 2.0-GHz processor with 1 GB RAM will be installed as a domain controller.
- Server 3: 2.0-GHz processor with 2 GB RAM will be installed as an application server.

Two links between the United States and Canada facilities will be available. They are as follows:

- A T-1 link for the primary connection
- A 256-Kbps link for a backup connection

Bandwidth should be used during the day mainly for file transfers and email. Any network maintenance that requires bandwidth should be done only between 11:00 PM and 4:00 AM on weekdays. Weekends are available anytime for maintenance procedures.

Sketch a design that will meet the previous requirements and consider the following questions:

- 1. Should you configure a bridgehead server at the Canada facility? If so, which server would you recommend?
- 2. What will you configure the costs for on each link?
- 3. What should the replication schedule and interval be set for?

### Scenario 3-2: Improving Replication Efficiency

You are the administrator for a mid-sized company network that consists of Windows Server 2008 domain controllers. The five sites you have are not fully routed, and there have been some problems replicating Active Directory data. You know your budget will not allow you to add additional links or purchase additional equipment. What can you do to improve the efficiency of replication within your network?

![](img/a8ee53dbf1310726255b6fbb9f296fb2_120_0.png)

# Global Catalog and Flexible Single Master Operations (FSMO) Roles

## OBJECTIVE DOMAIN MATRIX

| TECHNOLOGY SKILL | OBJECTIVE DOMAIN | OBJECTIVE DOMAIN NUMBER |
| :--- | :--- | :---: |
| Configuring Additional Global Catalog Servers | Configure the global catalog. | 2.5 |
| Placing FSMO Role Holders | Configure operations masters. | 2.6 |

## KEY TERMS

- cached credentials
- clock skew
- Domain Naming Master
- _gc
- indexed
- Infrastructure Master
- partial attribute set (PAS)
- Primary Domain Controller (PDC) Emulator
- relative identifier (RID)
- Relative Identifier (RID) Master
- Schema Master
- security identifier (SID)
- seize
- transfer
- universal group
- universal group membership
- caching

Margie's Travel is a national chain of booking agencies for resort hotels throughout Europe and the Caribbean. It relies heavily on Active Directory to provide authentication for its many database and intranet applications. Margie's Travel uses a multidomain Active Directory forest containing an empty forest root domain and several child domains representing the geographical regions served by the different offices. Because of the multidomain nature of the Margie's Travel Active Directory infrastructure, the Margie's Travel IT staff needs to strictly maintain access to global catalog servers and Flexible Single Master Operations (FSMO) role holders across the entire organization.

After completing this lesson, you will be able to discuss the global catalog server and the critical role that it plays within Active Directory. You will understand the importance of proper placement of global catalog servers within an Active Directory forest and how to add and remove global catalogs from your network. You will also be able to discuss a feature known as universal group caching, which can reduce the reliance on global catalog servers in certain environments where it might not be feasible to deploy as many as you require. Finally, you will be able to describe the Flexible Single Master Operations (FSMO) roles, and the functions that they perform within an Active Directory domain and forest. Through the exercises and information presented in this lesson, you will be able to plan the optimum placement of FSMO roles within your environment as well as to deploy, transfer, and seize FSMO roles in the event of temporary or permanent failure of one or more domain controllers within your Active Directory domain or forest.

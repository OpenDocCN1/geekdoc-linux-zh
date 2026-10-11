
## MANAGING DNS SERVER TASKS

As with most networking service consoles, such as WINS and DHCP, you can connect to other DNS servers. This feature enables you to easily manage a set of DNS servers from one location without having to physically visit each machine.

Typically, depending on the design of your organization, an administrator may be in control of all DNS servers for a particular zone. Remember that there is one primary DNS server per zone and any number of secondary DNS servers per zone. The secondary DNS servers provide load balancing for resolution requests. Through this one interface, you can manage all the DNS servers, which makes your job as an administrator much easier.

To connect to another DNS server, simply use the Action menu and enter the name or IP address of the DNS server. After the connection is made, the server’s icon appears in the console.

![](img/763d5ae436311371600c0952a3da9094_169_0.png)

![](img/763d5ae436311371600c0952a3da9094_169_1.png)

- 1. Select DNS in the console and choose Action→Connect To Computer.
- 2. Click the appropriate radio button to connect to either your server or another server.
- 3. If you chose to connect to another computer in Step 2, type the name or IP address of the server in this dialog box.
- 4. Click OK.

When you configured the DNS service, you made some decisions about forward lookup zones and reverse lookup zones. These zones help you control DNS on your network and make certain that host names can be resolved to an IP address or that IP addresses can be resolved to DNS names.

Zones also help you segment your network for administrative purposes. When you create zones, you must install a DNS server that will be authoritative for that zone. You can also use secondary DNS servers for the zone to help with load balancing.

You can easily add new zones to your server by using the New Zone Wizard. To perform this action, simply access the Action menu for the server and select New Zone. After you do this, the New Zone Wizard begins and you can create new zones as needed. This is the same wizard that you use when you set up DNS.

![](img/763d5ae436311371600c0952a3da9094_170_0.png)

![](img/763d5ae436311371600c0952a3da9094_170_1.png)

## ADDING NEW ZONES

- 1. Select the server in the console and choose Action::New Zone.
- 2. The New Zone Wizard appears.
- 3. Refer to the section Setting Up DNS for more information on completing the New Zone Wizard.

## MANAGING DNS SERVER TASKS

You can use the Action menu to clear the DNS server's cache. Remember that a cache is simply a temporary storage location that holds DNS temporary records. Clearing the cache allows you to remove those records so new records can be immediately cached.

You can also run a process that helps you keep a clean DNS database. This process, known as *scavenging*, cleans old records out of the database to make certain the database is up-to-date.

First, you can set the properties for scavenging by accessing Set Aging/Scavenging for all zones on the Action menu. The properties sheet enables you to configure the DNS server to scavenge stale DNS resource records. Then, you can set the no-refresh and the refresh interval. The no-refresh interval is the time between the most recent refresh of a record timestamp and the time when it can be refreshed. The default setting is seven days. The refresh interval is the time between the earliest moment when a record timestamp can be refreshed and the earliest moment when the record can be scavenged. The default is also seven days.

![](img/763d5ae436311371600c0952a3da9094_171_0.png)

- **CLEARING THE CACHE**
  - Select your server in the console, then choose Action→Clear Cache.

![](img/763d5ae436311371600c0952a3da9094_171_1.png)

- **OPENING A NEW WINDOW**
  - Select your server in the console, then choose Action→New Window From Here.

### Why do I need to scavenge the database?

As with any database, the DNS database can collect clutter over time. The clutter in the database is the old DNS records that have expired. The scavenge operation cleans these old records out of the database, which keeps your database free of unnecessary records.

### How often should the database be scavenged?

Under normal circumstances, the default setting of seven days for scavenge records is sufficient. You do not need to manually scavenge the database on a regular basis, unless you have specific reasons to believe the database needs to be cleaned. Windows 2000 DNS automatically scavenges the database every seven days, which under most circumstances is all you need.

### How does scavenging affect performance?

As with any system, the more "clutter" that is removed, the more likely the DNS service will perform better. By removing unneeded and old records, the DNS database will be clean of outdated information.

![](img/763d5ae436311371600c0952a3da9094_172_0.png)

![](img/763d5ae436311371600c0952a3da9094_172_1.png)

## CHOOSING THE AGING AND SCAVENGING SETTINGS

- 1. Select the server in the console and choose Action→Set Aging/Scavenging For All Zones.
- 2. Adjust the no-refresh interval as desired.
- 3. Adjust the refresh interval as desired.
- 4. Click OK.

## MANAGING DNS SERVER TASKS

You can manually update the DNS server's database files, if desired, by using the Action menu and choosing Update Server Data Files. Data files are normally updated to the database at predefined intervals and when the server is shut down, but you can choose to manually update the files as desired. This action causes the DNS service to write all changes to the zone data files immediately.

As with most MMC snap-in tools, you can also choose to stop, start, pause, and restart the DNS service by clicking the Action menu and accessing the All Tasks feature. In case of server maintenance or problems, you can pause or stop the service while the problem is being resolved. When you do this, the server is not available to answer name resolution queries, but other DNS servers in the zone can take on the query load while the server is offline.

![](img/763d5ae436311371600c0952a3da9094_173_0.png)

- **MANUALLY SCAVENGING DATABASE RECORDS**
  - 1. Choose Action > Scavenge Stale Resource Records to manually scavenge records.
  - 2. Click OK to continue the scavenge operation.

### Do I need to update the server's database files manually?

No. The DNS server automatically updates its server database files on a periodic basis, so manually updating the files is not a task you need to perform as a part of your administrative duties. However, the option is provided for you in the case of major changes to the DNS database. If a number of changes occur, you can use the Update Server database files option to manually update the database so those changes can go into effect immediately. As with most options in DNS, the server handles the tasks automatically, or you can manually force them as the need arises.

### What happens when I pause the DNS service?

When you pause the DNS service, the service is taken offline and is not available to clients. Client DNS query requests will have to be fulfilled by other DNS servers. The pause option is particularly useful if you are having problems with the server. You can take the server offline until the problems are resolved, then resume the DNS service.

![](img/763d5ae436311371600c0952a3da9094_174_0.png)

![](img/763d5ae436311371600c0952a3da9094_174_1.png)

## MANUALLY UPDATING SERVER DATA FILES

- 1. Choose Action > Update Server Data Files to perform the manual update.

## STOP, START, AND PAUSE

- 1. Choose Action > All Tasks.
- 2. Choose Stop, Start, or Pause to manage the DNS service.

## CONFIGURING SERVER PROPERTIES

You access the DNS server properties sheets to configure the various DNS functions that you want your server to perform.

Depending on the needs of your network, you may want to restrict a DNS server so that it only listens for query requests on certain IP addresses. This feature allows you to use a DNS server for a specific group of clients. You can enable this option, or simply allow the DNS server to listen on all IP addresses on the Interfaces tab.

The Forwarders tab enables you to configure *forwarders*—which is a DNS service that is configured to provide recursive service for other DNS servers. The forwarder helps other DNS servers resolve a DNS name request that cannot be resolved by forwarding the request to other DNS servers. If your server is the root DNS server, the forwarders option is not available because it is the root server.

![](img/763d5ae436311371600c0952a3da9094_175_0.png)

- 1. Select the desired server in the console.

![](img/763d5ae436311371600c0952a3da9094_175_1.png)

- 2. Click *Action* → *Properties*.

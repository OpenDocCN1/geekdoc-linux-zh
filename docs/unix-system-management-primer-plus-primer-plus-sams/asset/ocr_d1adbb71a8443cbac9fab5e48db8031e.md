# UNIX SYSTEM MANAGEMENT PRIMER PLUS

```
netapp snap create vol0 backup
netapp snap list vol0
Volume vol0
working......
```

| %used | %total | date | name |
| 0% (0%) | 0% (0%) | Mar 07 20:30 | backup |
| 2% (2%) | 1% (1%) | Mar 07 20:00 | hourly.0 |
| 11% (6%) | 6% (5%) | Mar 07 16:00 | hourly.1 |
| 14% (5%) | 8% (2%) | Mar 07 12:00 | hourly.2 |
| 15% (0%) | 8% (0%) | Mar 07 08:00 | hourly.3 |
| 16% (2%) | 9% (1%) | Mar 06 20:00 | nightly.0 |
| 20% (5%) | 12% (3%) | Mar 06 16:00 | hourly.4 |
| 20% (1%) | 13% (0%) | Mar 06 00:00 | nightly.1 |

This listing also shows the trend of storage requisites for multiple snapshots. As time goes on and more data changes, older snapshots take up an increasing amount of space as they have to retain more of the original data.

![](bbox=[0.118, 0.425, 0.185, 0.465])

# Real-World Example: Snapshots at the Office

One company used NetApp Appliance filer for both its Unix and Windows file shares. Snapshots were taken six times during the work day, so that anyone who accidentally deleted a file or saved a change they didn't mean to easily restore a previous copy of the file from the last snapshot.

# Using Multiple Network Paths

A network is just as likely to fail as any other component in your infrastructure. You can easily understand the potential for network failure when you consider the number of parts in a network that could fail, including cables, routers, switches, NICs, and telco lines. Highly available networking can be achieved by configuring redundant network paths between your critical systems and between your systems and the Internet.

# Provider Redundancy

Sites with a single telco to the Internet risk losing connectivity if that line goes down. Many time connectivity problems lie with your provider or the phone company, leaving your business in the hands of a potentially overworked and under-responsive staff if disaster strikes. One way around this situation is to use multiple providers for your Internet connectivity. Many ISPs use several links to different major, tier-1 backbone providers such as UUENet, AT&T, and Sprint to provide virtually uninterrupted connectivity. An ISP's routers will simply reroute traffic to other network paths when one becomes unavailable.

## Unscheduled Outages

An unscheduled outage is any outage which occurs without warning. Even the most watchful and careful system administrator can expect to experience unscheduled outages on his or her network. The cases for unscheduled outages take many forms, such as a configuration glitch, hardware failure, human error, or even a building going up in flames.

Human error is one common cause of unscheduled outages. Some examples of human error that could cause an outage are as follows:

- Typing the wrong command as root
- Disconnecting the wrong cable from a server
- Making a typo in a configuration file
- Experimenting with new software or configurations on a production server

Most error can be prevented if the system administrator and other technical staff take extreme care when working with around production systems. Double check all changes that you make, or even better, use a change management system to approve and communicate your changes ahead of time. See Chapter 14, "Internal Communication," for more details on change management.

Whatever the cause of an unscheduled outage, the events that prompt the maintenance are unexpected. Most unscheduled outages are out of the system administrator's control, as is the amount of downtime they cause. Minimizing the downtime incurred by an unscheduled outage is one of many challenges a system administrator faces.

![](img/894492738e879267320b8d6f9a044180_222_0.png)

## Document Outage Procedures

When you experience and resolve an unscheduled outage, document the procedures you took to solve the problem. You are likely to experience the outage more than once, and having documentation up front will help improve the response time for subsequent outages.

## Real-World Example: Human Error Outage

> Real-World Example:
> An administrator at an ISP was decommissioning an old server in a densely populated rack, and the administrator needed to unplug the server's power cable. The server's cables were not labeled, and the administrator mistakenly pulled the power cable for a Network Appliance filer that served email and Web site data for 60,000 users. This caused a massive outage. Needless to say, it was heartbreaking for the administrator to hear the critical fans stop spinning! The filer was plugged back in and the administrator verified that everything functioning properly before removing the old server. The outage lasted for five hours, but was monitored by many of the system's 60,000 users. This outage had to occur; had the administrator labeled the cables and taken the time necessary to trace the proper cable in a densely populated rack that contained business-critical hardware, he could have avoided this embarrassing and potentially costly outage. In fact, the next day the organization organized a cable labeling project to prevent this kind of mistake from happening again. However, even in well-designed systems, human error can bring everything crashing and is the cause of more unscheduled outages than one is willing to admit.

## Partial Service Outages

Some services provide only a single function. For example, POP has the sole purpose of allowing a user to download mail from a mail server. A system administrator can easily determine when a single-function service is down and the repercussions of that outage for the business. In the POP example, an outage means users get an error message when they try to download their mail.

Other services provide more functionality and, therefore, can present a more complex diagnosis and maintenance issue. A Web server, in addition to providing simple static Web pages, can also support file uploading, CGI scripts can process forms, and code on the back end interface with databases. Each does SSL to miss, and you have an entirely secure Web server. Each Web server has its own unique functions, turning the simple HTTP protocol into a complex internet service.

When somebody reports a Web server outage, the system administrator may have no clear idea what is causing the outage or what services the outage has taken down with it. Is the entire Web site down, or is just one part of the site? Is one script failing, or is there a database on the back end?

Complex services (such as this Web server example) can experience service outages where the service as a whole is up and running, but parts of the service are failing. For example, a banking Web site might be available on the Internet, but the pages that let you check your account balances produces an error. For these complex services, the sooner you understand what part of the service is down, the better you will be able to resolve the problem and the non-functioning part of the service—and the responsibility for helping users supply this information to help pinpoint the problem lies with your help desk. Help desk staff should ask users to describe exactly what they were doing when they experienced the problem, as well as any error messages they received. The more detailed the problem report, the easier it will be for you to track down a small problem with a large service.

## Automatically Generated Error Reports

Many applications and operating systems provide a mechanism for automatically generating detailed error reports and sending them to the vendor's help desk. Although no Unix operating systems offers this yet, Network Appliance filers (network file servers) provide an "autosupport" functionality in which system status is periodically emailed to Network Appliance support, including after every reboot or crash. This report helps support staff gather evidence that you would normally have to provide yourself, as well as allowing them to see potential problems before they cause an outage.

![](img/894492738e879267320b8d6f9a044180_223_0.png)

## Complete Outages and Degraded Service

A complete service outage is the nightmare all administrators fear. In a complete service outage, a service is 100% unavailable to its users. These outages are all too often the cause of 3:00 a.m. on a Saturday.

Not all outages are catastrophic as just described. Sometimes problems just cause a service to become degraded. Much as a power brownout causes lights to dim but not fail, users can still use a degraded service; it doesn't perform as well as it normally would.

A POP3 service example can help illustrate degraded service outages. Users of these servers are used by clicking on a "Retrieve Mail" button on their clients and receiving their mail within seconds. However, during an outage in which the mail server is overloaded with incoming mail, users experience delays up to two minutes before receiving any messages. Another two-minute delay separates subsequent message retrievals. While the mail service is working, it is painfully slow, and not practical to use.

Other examples of degraded service include the following:

- Slow Web server response due to excessive network traffic
- A single failed Web server in a pool of servers, causing every couple of HTTP requests to fail
- An application causing excessive paging, slowing down other services on the same server

![](img/894492738e879267320b8d6f9a044180_224_0.png)

## Service Monitors Detect Degraded Services

As you learned in Chapter 6, service monitors can detect degraded service using timeouts. If, in the POP3 example just given, the system administrator had used NetSaint’s POP3 service monitor and set its timeout to 30 seconds, the administrator would have received an alert for two-minute delay.

Degraded service, while not a complete outage, still causes significant problems for users. Degraded service problems can be the most difficult to diagnose, because the system is working functionally; you have to find the parts that are failing, investigate the causes and fix the problems.

Degraded service usually indicates that one or more parts of the service are under stress. In the earlier example, the POP3 service was slow. The logical place to start looking for problems in that situation is in the server itself. Many subsystems can be stressed on a Unix server, including CPU, disk, network, and memory, and the system administrator must examine them all to find the problem. Chapter 11 discusses such diagnostic examinations in detail.

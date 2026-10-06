
Effective Monday January 28 at 7 AM, access to corporate servers via telnet will no longer be permitted. Please use the new SSH client available from the IT home page. Detailed instructions are included in the attached document. Please contact the IT department at helpdesk@example.com if you experience any problems.

Thank you,

The IT Staff

## Arrange for Backups of the Original Service's Data

Before beginning any decommission, ensure that you have (or plan to take) full backups of the original service's configurations and data. Some data is bound to be lost or configurations forgotten over the new system, and these will not be available after the old service is decommissioned and its systems have been repurposed.

## Easing into Any Transition

Most users do not react well to abrupt changes; they need a transitional period in which they can adjust to the usage and quirks of any new services. This transitional period can range from a few hours to a few years, depending on the scope of the service you are offering and the urgency of the change.

The most publicized decommission in progress as of this writing is the transition from analog television broadcasts to digital broadcasts. Currently, the process is in its infant stages, but the FCC (Federal Communications Commission) has declared that all NTSC (National Television Standards Committee) broadcasts, which are the analog standard in 2002, will be phased out completely in favor of digital broadcasts by 2006.

The transition from analog to digital technology means major changes not only for television networks, but also for consumers; every television manufactured and sold in the country must be able to receive digital broadcasts by 2006. Considering the millions of television consumers buy every year in this country, the transition represents a major task. Digital TV broadcasts began in 1998, so the FCC has implemented an eight-year transitional period for consumers and television networks to adopt the new technology. That's a long time, but it gives everyone a chance to catch up and adjust to the new technology in time for the official decommissioning.

The same kind of careful planning and transition phase is essential for a successful IT decommissioning project. Corporate users need information, assistance, and ample time to adjust to the adoption of new technologies or the loss of old technologies to which they've become accustomed. In general, there are four major steps to follow during a transition:

- Notify users and management of the impending decommission. Include the services that are being decommissioned, the time of the decommission, and the length of any transition period in which the old services can still be accessed.
- Install and configure the replacement systems ahead of time and test their functionality stability.
- Allow end users to test the new system before the decommission takes place.
- Provide ample transition time for training and system tweaking before the old system is turned off for good.

Consider the example of an IT department in a company whose employees traditionally use telnet to connect to the corporate network from home. The company’s CTO has decided that using Telnet is too insecure and limited. The CTO declares that a VPN (virtual private network) solution should be in place within three months, at which time Telnet access is to be disabled.

Two months are ample time for system administrators to have a VPN solution in place. But they don't rush the system into it immediately. Decommissioning Telnet won't give you the other staff much time to adjust. Instead, the IT department sends out informational notices concerning the eventual Telnet decommissioning, beginning early in the three-month transition period the CTO has declared. Then, after the new VPN system is ready, the IT department uses the final month of the transition period to slowly phase out Telnet.

During the month-long end-user transition, IT issues VPN clients to staff accompanied by detailed instructions. It also arranges VPN software for creating desktop support staff, so they can provide support to the inexperienced users. During this one-month transition, Telnet access is left open while everyone gets to use the VPN. This "dual service" also leaves a proven viable remote access solution in place during the transition—if users begin to experience problems with the VPN, they can fall back to Telnet while administrators fix it. After the month is up, an announcement can be made that Telnet is finally being decommissioned.

## Create a FAQ for the Transition

During the transitional phase, you may discover problems and questions that are common to most users. Create a FAQ that provides answers and solutions to the end users and post it somewhere easily accessible, such as a company intranet, or distribute it via email.

## Decommission, Don't Destroy

When most people finish reading a good book, they might put it back on a bookshelf or even pack it away in a box, but rarely do they toss the book in the trash. You can think of decommissioned services as being similar to those used books: Even though you're no longer using a service, you don't rush to destroy its data or break its server down for spare parts, at least not immediately. What happens if something goes wrong with your new deployment a day, a week, or even month down the road? What if you need data from the old server that isn't in your current backup library?

# Chapter 7 • PATCHES, UPGRADES, AND DECOMMISSIONS 195

It's a good idea to keep the infrastructure from the old service up and running, or at least available to administrators, for a period of time after its decommission. With the old infrastructure on reserve, you can still retrieve data from or revert back to the original service if something goes horribly wrong with the new service. When you've had ample time to determine that the old service is completely obsolete and supplanted by the new service, you can repurpose the infrastructure.

## Summary

Patches, upgrades, and decommissions are not very exciting parts of system administrator's day. Too often, system administrators ignore these basic functions. As this chapter has explained, all changes to network require careful planning, testing, end-user, and follow-up. To plan and implement a successful decommission, follow these general rules:

- Read all documentation.
- Know who is using the services.
- Test everything in sandbox environment first.
- If you don't have sandbox, lobby for one.
- Notify users and management of upcoming changes.
- Back up systems completely.

## Review Questions

1. Why should sandbox mimic production environment?
2. Why is it advisable to patch operating system in single-user mode? What steps you take if you are unable to bring your system to single-user mode?
3. What is shared library and why is it an important part of system upgrade?
4. How would you replace disk in server that does not support hot-swapable disks? What would be the procedure if the server did support hot-swapable disks?
5. What are three ways system administrator can determine the end users of particular service?

# CHAPTER 8

# SERVICE OUTAGES

You will learn about the following in this chapter:

- The seven most common types of service outages and their causes
- How to schedule maintenance for minimum business disruption
- Best practices for performing maintenance within scheduled outage times
- Assessing service performance for compliance with service level agreements
- Effective procedures for responding to and resolving service outages
- Analyzing the root causes of service outages

Information technology is the bedrock of most organizations. Revenues, production, scheduling, sales, and many other business functions rely on fully functional IT services. Service outages can represent tremendous losses—in revenues, personnel time, customer goodwill, and important business commodities. As such, even those that are necessary for routine maintenance or system repair—are considered by most to be the great evil of information technology. As a system administrator, your company expects you to rise up and quickly resolve every outage whether it occurs during 9-to-5 working hours, or at 3:00 a.m. on Saturday. System administrators are on-call heroes who faithfully respond to outage notifications and quickly get systems back up and running, in order to minimize losses to the organization. All too often, in fact, system administrators are recognized more for their performance during outages than for the time and energy they invest in designing and implementing system infrastructures that suffer from a minimum of such outages. chapter discusses some common types of Unix service outages and how you apply them, to the Unix system administrator, and your business. You learn about the metrics surrounding outages, including maintenance windows and service level agreements. And you learn the most effective procedures for dealing appropriately with outages and how to use each outage as a learning tool that can help you minimize similar outages in the future.

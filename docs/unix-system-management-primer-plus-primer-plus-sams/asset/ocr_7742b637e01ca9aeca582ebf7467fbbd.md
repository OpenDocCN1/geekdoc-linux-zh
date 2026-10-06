# UNIX SYSTEM MANAGEMENT PRIMER PLUS

It may not be your responsibility to make sure everyone remembers what you've told them about upcoming activity, but any help you can provide in this area helps to minimize problems resulting from users being unprepared for the activity. One resource that you can offer is a system activity schedule that documents all scheduled maintenance activities. Users can check this schedule at their leisure to find out when you have system activities. If they've lost that email you sent out last week, they will still have fast, easy access to the information.

If you are lucky enough to have a help desk, the help desk staff can maintain the system activity schedule. That arrangement relieves you of the burden of maintaining the schedule, and it creates a centralized scheduling authority. When somebody adds an event to the schedule that conflicts with another event within the organization, the help desk can quickly point out that and resolve the issue with both parties.

If you are stuck coordinating these activities on your own, document all of your planned activities in calendar or planning software, such as Microsoft Project or Microsoft Exchange. If your organization has already standardized on this type of software, use that so you can integrate your system with schedules for other groups.

![](bbox=[0.137, 0.433, 0.193, 0.473])

# Publicize Scheduled Activities

Post a copy of planned system activities on a public bulletin board or your company's intranet—anywhere it will be seen on a daily basis. This will enable casual passersby to see what is scheduled for your group without having to start programs on their computer or browse the company intranet. Update it regularly (at least once a week) so the information is always current.

# Naming Conventions

Even hostnames can be a form of communication, albeit a very subtle one. Hostnames should be self-documenting as possible, so you can determine the purpose of any machine on your network from its name alone.

System and network administrators tend to name devices on their network according to the following three conventions:

+   * Functional naming is useful for devices that have specific purposes—a Web server, for example, or a DNS server. You might name your servers web1, web2, and web3, while your name servers are called ns1 and ns2. These names clearly indicate the function of each system while uniquely identifying each individual machine.
* Geographical naming is useful in organizations with multiple physical locations. Large ISPs often use geographical naming, especially backbone providers that have network all over the country. For example, an ISP's core routers in Philadelphia, Pennsylvania and Ann Arbor, Michigan might be called phl-core1 and aa-core1.
You can, of course, always console your ego by diving into the network of a Fortune 500 company that regards Windows XP/2003 as a precious, endangered species to be preserved at all costs, but the tide is catching up to you. You know in your heart that you have to move on to brighter shores.

At the end of the day, that's what hacking is all about. The frustration of having to throw away a favorite trick can only be matched by the exhilaration of mastering a shiny new technique.

We loosely define *hacking* as an ensemble of tricks and tips designed to achieve unexpected results from a system or a process. Yet, these tricks have an ever-accelerating expiry date. Your aim as a security professional or enthusiast is to seek out and gather as many useful tricks as you can. You never know which spear will stop the bull's charging ahead.

In my other books, I focused a great deal on Windows-related attacks, because most of the Fortune 500 companies designed the majority of their environment around Active Directory. It was the go-to solution to manage thousands of users, servers, and applications.

The zeitgeist is changing, though. A company looking to set up its infrastructure from scratch will no longer spring up a Windows Domain Controller on bare metal in a shared datacenter 20 miles from the city. Really, show me a system admin who still wants to manage hardware obsolescence and an ESXi cluster with 30 appliances with different firewalls, switches, routers, and load balancers. Hand me that noose and close the door already!

Why bother when you can set up everything in a cloud environment in a matter of seconds? Databases, Docker containers, and Active Directory are all but one click away, with a free trial to sweeten the deal for your accountant. Sure, the initial low-ticket fee quickly balloons as your servers scale up, but most startups will be delighted to deal with these types of problems. It means business is growing.

In this book, I have decided to throw away the conventional architecture you find in greasy old companies. Let's see how an attacker might take down a modern and worthy opponent: a company that planted its technical roots in a nurturing and resilient cloud environment, and powered its growth using DevOps practices.

Beyond buzzwords touted by clueless management and hungry headhunters, when followed successfully these new paradigms have such a deep impact on architectural decisions and application designs that they naturally require a new set of tricks and flair to hunt for and find loopholes. Vulnerabilities that may otherwise be overlooked or dismissed in a classic environment suddenly acquire lethal potential in a cloud setting. Forget SQL injection. The second you know that a machine is hosted on Amazon Web Services (AWS), you should focus on another class of vulnerabilities altogether.

Attackers used to hop from one machine to another, sneaking past firewall rules and burrowing their way to the internal database, Active Directory, and what have you. This journey often involved network scans,
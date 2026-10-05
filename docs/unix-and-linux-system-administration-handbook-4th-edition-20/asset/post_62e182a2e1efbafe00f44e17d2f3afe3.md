
# Standardized documentation

Our experience suggests that the easiest and most effective way to maintain documentation is to standardize on short, lightweight documents. Instead of writing a system management handbook for your organization, write many one-page documents, each of which covers a single topic. Start with the big picture and break it down into pieces that contain additional information. If you have to go into more detail somewhere, write an additional one-page document that focuses on steps that are particularly difficult or complicated.

This approach has several advantages:

- Your boss is probably only interested in the general setup of your environment. That is all that's needed to answer questions from above or to conduct a managerial discussion. Don't pour on too many details or you will just upset your boss to interfere in them.
- The same holds true for customers.
- A new employee or someone taking on new duties within your organization needs an overview of the infrastructure to become productive. It's not helpful to bury such people in information.
- You can index pages to make them easy to find. The less administrators have to spend looking for information, the better.
- It's easier to keep documentation current when you can do that by updating a single page.

This last point is particularly important. Keeping documentation up to date is a huge challenge; documentation is often the first thing to be dropped when time is short. We have found that a couple of specific approaches keep the documentation flowing.

First, set the expectation that documentation be concise, relevant, and unpolished. Cut makes the documentation sphincter snap faster than the prospect of writing a dissertation on design theory. Ask for too much documentation and you may not get any. Consider developing a simple form or template for your sysadmins to use. A standard structure helps to avoid blank-page anxiety and guides sysadmins to perform pertinent information rather than fluff.

Second, integrate documentation into processes. Comments in configuration files are some of the best documentation of all. They're always right where you need them, maintaining them takes virtually no time at all. Most standard configuration files allow comments, and even those that aren't particularly comment friendly can often have some extra information sneaked into them.

# Hardware labeling

Locally built tools can require documentation as part of their configuration information. For example, a tool that sets up a new computer can require information about the computer's owner, location, support status, and billing information if these facts aren't directly relevant to the software configuration.

Documentation should not create information redundancies. For example, if you maintain a site-wide master configuration file that lists machines and their IP addresses, there should be no other place where this information is updated by hand. Not only is it a waste of your time to make updates in multiple locations, but inconsistencies are also certain to creep in over time. When this information is required in other contexts and configuration files, write a script that obtains it from (or updates) the master configuration. If you cannot eliminate redundancies, at least be clear about which source is authoritative. And write tools to catch inconsistencies, perhaps run regularly from cron.

The advent of tools such as wikis, blogs, and other simple knowledge systems have made it easier to keep track of IT documentation. Set up a single location where all your documents can be found and updated. Don't forget to get it organized, however. One wiki with 200 child pages in one list is cumbersome and difficult to use. Be sure to include a search function to get the most out of your system.

# Hardware labeling

Some documentation is most appropriate when written out on a piece of hardware. For example, emergency procedures for a system or network failure are not particularly useful if they are stored on a dead or unreachable machine.

Every computer should be identifiable without someone's switching it on and logging in, because those activities will always be possible. Uniquely label each workstation, server, printer, tape drive, and piece of network equipment. Labels should include the item's name and IP address (if it has one). Labels for peripherals should identify the host on which they live and the device files through which the device is accessed.

In a server room it is useful to have these labels on both the front and the back of the machine (especially in cramped racks) so that you can easily find the switch of the machine you want to power-cycle.

If your environment includes many different types of systems, it may be useful to add additional information such as architecture, boot instructions, key sequences, pointers to additional documentation, the vendor's hotline, or the phone number of the person in charge. Recording key sequences may seem a bit silly, but servers are often connected to a console server rather than a dedicated monitor, and administrators need to know how to get to the correct system.

# Chapter 32 Management, Policy, and Politics

Be sure your central records and inventory data contain a copy of the information included on all these little sticky labels. This data is handy if you manage your machines through a TCP/IP connection to your console server instead of spending your work day in a noisy machine room.

In cases with extensive machine-specific data, you might consider deploying a bar coding system that lets you pull up all the relevant details for a device on a mobile laptop. (Of course, that mobile system shouldn't itself depend on a properly functioning network or database server).

# Network documentation

Network wiring must be scrupulously documented. Label all cables, identify patch panels and wall outlets, and mark network devices. Always make it easy for your technicians to keep the documentation up to date; keep a pencil and forms hanging on the wall of wiring closets so that is painless to note that a cable can be moved from one device to another. You can transfer this data to on-line storage at regular intervals.

Most network devices (e.g., routers and switches) can be reconfigured over your network. Although you can now move machines among subnets from your cozy office, documentation becomes even more important. Be careful, because you can now screw up a much bigger part of your infrastructure more quickly and thoroughly.

You might consider using a software package such as Rancid to help keep track of your device configurations. These tools also catch accidental and forgotten changes, which can drastically reduce unplanned downtime.

# User documentation

Prepare a short document that you can give to new users. It should document local customs, procedures for reporting problems, the names and locations of printers, your backup and downtime schedules, and so on. This type of document can save an enormous amount of sysadmin or user time. You should also make the information available on the web. A printed document is more likely to be read by new users, but a web page is easier to refer to at time questions arise. Do both and keep them updated regularly. Outdated-on-line documentation or FAQs are worse than useless.

In addition to documenting your local computing environment, you may want to prepare some introductory material about UNIX for your power users. We provide printed one-page crib sheets that list the commands and applications needed by your user community.

# Keep environments separate

Organizations that write and deploy their own software need separate development, test, and production environments so that releases can be staged into

# Automate, automate, automate

general use through a structured process. Separate, that is, but identical; make sure that development systems are updated, the changes propagate to production environments as well. Of course, the configuration updates themselves should be subject to the same kind of release control. "Configuration changes" includes everything from OS patches to application updates and administrative changes.

It is critical to protect your production environment by enforcing role separation throughout the promotion process. For example, the developers who have administrative privileges in the development environment should not be the same people who have administrative and promotion privileges in other environments. A disgruntled developer with code permissions could conceivably insert malicious code at the development stage and promote it to production. By distributing approval and promotion duties to other people, you require multiple people to collude or make mistakes before problems can find their way into production.

Document your code promotion process and follow it religiously. Don't make exceptions. If you find that the regular process is not efficient enough for emergency changes, document an emergency change process and make sure it is followed. You should also audit the code promotion process and go back and make adjustments where necessary.

Developers are sometimes frustrated by the level of documentation required in this type of system. Consider holding some lunch-and-learn sessions to help them understand the motivations for your requirements. Developers who are bought as co-conspirators are more likely to follow the standard procedures.

# Automate, automate, automate

Your site-wide management system should contain the following major elements:

- **Automated setup of new machines:** This is not just OS installation; it includes all the additional software and local configuration necessary to allow a machine to enter production use. It is inevitable that your site will need to support more than one type of configuration, so include multiple machine types in your plans from the beginning.
- **Systematic patching and updating of existing machines:** When you identify a problem with your setup, you need a standardized and easy way to deploy updates to all affected machines. Note that computers are not on all the time (even if they are supposed to be), your update schedule must correctly handle machines when the update is initiated. You can check for updates at boot time or on a regular schedule; see Chapter 12 for more information.
- **A monitoring system:** Your users should not have to call you to tell that the server is down. Not only is it unprofessional, but you have no idea how long the system has been down. The first person to call you is
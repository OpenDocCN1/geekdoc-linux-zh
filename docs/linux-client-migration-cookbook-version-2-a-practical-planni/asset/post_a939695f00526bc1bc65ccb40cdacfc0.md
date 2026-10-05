
collaboration between users, and data migration is unnecessary. Connecting desktops to a file server can be as simple as mapping a Windows share (perhaps using a Linux server running Samba and requiring all users to keep their data in that directory. Laptops are more difficult, because users want their documents available when they are away from the office. Using a synchronizing system like Novel's Folder can solve the problem. If a user's files are all stored in the network server, you only need to connect the new Linux desktop to the same server, and all of the user's documents are available on the new machine.

For some reason files cannot be stored in the network, then it helps to implement a policy which requires files to be in a specific directory structure on each machine. For instance, users could be told to keep all of their documents in the My Documents directory. Then, during a migration copying the My Documents to the new Linux desktop ensures that all the necessary documents are on the new machine.

## 6.3 Central mail server

Just like storing files in the network, using a central e-mail server provides many of the same benefits. There are numerous open source mail servers which provide IMAP. However, these servers only centralize e-mail and not the storage of contacts, calendar, and tasks. To centralize these features, a groupserver is required. There are still many choices from open source servers such as Open-Xchange, OpenGroupware and the upcoming Hull project from commercial servers such as Novel Groupwise, Scalix, or even Microsoft Exchange. Not all groupware servers support all e-mail clients, so more investigation into the available options is required. The user stores all e-mail, contacts, and calendar information about the groupserver, the migration of this data only requires setting the account information about the new Linux desktop.

## 6.4 Break down migration into manageable groups

Replacing the operating system and applications on every computer in an organization is a daunting task. Not only is it usually not to replace every machine in one step, it is certainly unwise. Before a migration, you break the task of migration into smaller, more manageable tasks. It makes sense to start with the easiest groups to migrate, then continue on the line. For instance, you might want to move your call center (which only requires e-mail and Web access) first, after that, the sales team (which also requires an office suite), and then marketing (which requires graphics tools). You probably want to break each of those groups into smaller groups, such as project or by location. It is important to ensure that each of the groups that have been migrated can still operate with those that have yet to be migrated. If two groups need to work with each other, cannot work together during a migration, then there is unnecessary animosity directed towards the Linux desktop, either combine the groups into one, or find a solution to their interoperability needs. This might require a migration to a transitional desktop setup, which was described in 6.1, "The transitional desktop" on page 132. A sample breakdown is shown in Figure 6-1.

![](img/23b949da14ff7bab8762f0f0361af394_162_0.png)

## 6.5 Minimize impact of down time

One of the most expensive results of a migration is down time. Any time users are not able to perform their job duties is lost productivity that costs the company money. While there is never a perfect time for a disruptive migration, minimizing the amount and impact of down time is key. One option is to do migrations during the evening or weekend off-hours. This might require paying overtime or other compensation to the IT staff, but it could severely minimize the outages. Depending on the size and skill set of the group migrating, the migration could be performed during an all-day training session. This, the users could return from the training session to start using their new Linux desktops.

Figure 6-1 A sample breakdown of down time

## 6.6 Get user feedback

Before migrating a group of users, select a representative minority to give feedback on the proposed Linux desktop solution. Ensure that the users will be able to perform all the necessary tasks for their jobs under the new operating system. Try to see if the users can perform these tasks without help. Listen to the problems that the users face and try to solve the underlying problem. For instance, users might complain that the new desktop cannot perform certain tasks, in reality, they do not know how to perform the task or solve the problem. Use what you learn from the users' problems to fix the desktop solution or to tailor the training classes to focus on problem areas.

After migrating each group, learn from any mistakes that happened, and plan better for next group. You might decide to offer more in-depth training or to change your installation methodology.

## 6.7 Automate the migration

Users have an easier time adjusting to the new operating system if their data and personalized settings have been applied to the new machine. Custom scripts can be written to copy data from the users' My Documents and Desktop directories and to set up any of the settings on the new desktop. However, there are hundreds to thousands of settings that users can have customized on their desktop. There are commercial tools, which can automate migration of settings such as the user's wallpaper or screen saver settings, and application settings, as e-mail messages and accounts. Internet bookmarks and home page, custom dictionaries in word processor programs, or instant messaging accounts. These tools also handle the migration of data, either from specified directories or the ability to search by file type over the entire hard drive. More information about a tool like this, Desktop from Versora, is available in Appendix C, “Automating desktop migration using Versora Progression Desktop” on page 277.

## 6.8 Use a systems management tool

Systems management tools, such as IBM Tivoli Provisioning Manager¹, Red Hat Network², and Novell ZENWorks Management³ provides features such as automated installation of software, or even full system deployment through provisioning modules. Can also be used to schedule the execution of custom jobs, such as running an automated migration on multiple machines at once (an example of this is described in 6.7, "Automate the migration" on page 136). Studies have shown that by leveraging an enterprise management tool and an automated migration tool, one technician can complete migration of one hundred or more desktops in a single day, as opposed to much fewer if the process was managed manually.

**Important**: For medium to large enterprises, you can expect that the business case for a migration cannot be entirely justified by a potential cost for savings in operating system and application licensing fees. In fact, in a client migration scenario, you should expect that the most important consideration that will come into play will be the overall cost of *managing* the client computing infrastructure on an ongoing basis.

As the size of the supported client base scales up, these costs (IT staffing, support and help desk, system upgrade and repair protection from viruses and others, and so forth) greatly outweigh the costs of recurring operating system and application software licensing.

This is why we strongly recommend that the approach for building a cost justification model for a client migration to Linux shows the potential for introducing innovative ways to achieve savings in how enterprise client platforms are managed. The integrated management tooling suites by strategic IBM Business Partners, such as Novell and their ZENWorks Suite and Red Hat and their Red Hat Network, provide important value added features that any enterprise must consider implementing as part of a Linux client migration plan.

Not only do systems management tools help in the installation and migration of Linux desktops, but they can also help to maintain these desktops throughout their lifecycles. More about systems management tools can be found in Appendix B, "Using enterprise management tools" on page 255.

## 6.9 Do not migrate until you are ready

Replacing an operating system is a difficult task. It should not be done lightly, or without sufficient planning. Even then, Linux might not be the perfect solution for some users (such as those with many irreplaceable applications, or laptop users whose power management, sound, and wireless drivers are not supported under Linux). It might be necessary to have a mixed network of Linux, Windows with only commercial software, and Windows transitional desktops. While this setup¹ http://www-306.ibm.com/software/tivoli/products/prov-mgr/
² http://www.redhat.com/rhn/
³ http://www.novell.com/products/zenworks/linuxmanagement


# Chapter 20: Backups and Disaster Recovery

449

+   - In case of system crash on either server, reboot the system and check the log file to determine the cause of the failure. All systems are restarted automatically by the initialization scripts, so everything should come up Dave at 555-1234 if the Web server doesn't seem to come up correctly.

+   - In case of a problem with the ISP connection, switch the router immediately to the secondary ISP connection, making internal traffic of lower priority. Contact our ISP, Netcom, at 1 800 555-6789 and ask for Richard P. If the problem is with phone lines, contact our U.S. West representative, Jill, at 1 800 555-7890.

# ## Implementing Your Plan

Obviously, all the details of the above plans are not included, especially in the second one. But the examples outline some of the issues of backup and recovery and how you can protect your systems at many different levels. Much more complex plans are in use at large companies all over the world. In fact, if you are in a large organization, the best way to start working on your Web disaster plan is to contact your MIS department and ask staff members for help. They may have many of the issues resolved for their existing systems. You'll just need to adapt them to your hardware and add the Internet access to the plan.

The scope of disaster planning is very large and fills many specialized books. This type of planning can be for a vital Web site and what types of things you can do to protect your investment and effort. If you really need to keep your Web server up all the time, you should seek additional information about system maintenance and disaster planning from other publications and computer groups as CERT, the Computer Emergency Response Team (see http://www.cert.org).

# ## Backing Up Your Web Server

If your computer is used only as a Web server, performing backups is a lot easier than backing up a regular Linux server. This is because most of the data that changes on your Web server is contained in a single subdirectory: /home/httpd/html.

Of course, that oversimplifies the layout of many more diverse Web servers, but you can still see that backing up your Web server doesn't need to be complicated.

# ## Types of Backups

The reason to back up your Web server is to be able to restore the system to its previous condition if a system failure causes part of the data on your hard disks to be
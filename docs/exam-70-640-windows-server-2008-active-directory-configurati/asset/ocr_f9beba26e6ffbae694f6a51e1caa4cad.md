+   3. Intersite replication uses \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ traffic to reduce the impact to bandwidth on corporate WAN links.

+   4. The KCC creates a(n) \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ to allow replication to take place in the opposite direction in the event that a single domain controller in the replication topology fails.

+   5. The purpose of the KCC is to create a(n) \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ between multiple domain controllers within a site as well as between sites.

+   6. By default, all Active Directory site links are \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_.

+   7. When Active Directory detects a replication conflict in which two objects have been modified nearly simultaneously, the first attribute that Active Directory will use as a tie-breaker is the \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_.

+   8. Active Directory will designate a(n) \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ within each site to manage intersite replication activity.

+   9. The minimum \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ that you can assign to a site link is 15 minutes.

+   10. Within a single site, domain controllers will use \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ to inform other DCs that intrasite replication needs to take place.

# Multiple Choice

*Circle the correct choice.*

+   1. The KCC is responsible for calculating intrasite replication partners. During this process, what is the maximum number of hops that the KCC will allow between domain controllers?
+   	a. 2
+   	b. 3
+   	c. 4
+   	d. 5

+   2. Replication that occurs between sites is called \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ replication.
+   	a. Local
+   	b. Remote
+   	c. intersite
+   	d. Intrasite

+   3. Company XYZ is a national company with locations in Detroit, Minneapolis, Phoenix, and Dallas. There are two connections between Detroit and Minneapolis. The first is a T-1 link and the second is a 128-Kbps link. When setting up the site links for replication, what should you do to ensure that the 128-Kbps link is used only if the T-1 is unavailable?
+   	a. Set a cost of 1 for the T-1 and a cost of 5 for the 128-Kbps link.
+   	b. Set a cost of 5 for the T-1 and 1 for the 128-Kbps link.
+   	c. Leave the costs at their default value of 100.
+   	d. Change the schedule manually to disallow replication on the 128-Kbps link until it is needed.

+   4. You are the administrator for a network that has several sites. There is a site link from the main headquarters to each remote site for file transfer and replication purposes. You have been asked to create five new users on the network, and several of the users need immediate access to network applications. When asked by your manager how long replication of these new accounts will take, what is your response?
+   	a. Replication occurs every 180 minutes by default.
+   	b. Replication occurs at 15-minute intervals.
+   	c. Replication occurs as soon as the account is added.
+   	d. Replication occurs only between 12:00 AM and 6:00 AM.
# Figure 3-8
Inter-Site Transports folder

![](bbox=[0.31, 0.06, 0.73, 0.22])

+   2. Right-click the desired protocol, either IP or SMTP, and select New Site Link.
+   3. In the New Object-Site Link dialog box, key the name of the site link. This name should reflect the locations that will be connected using this link.
+   4. From the Sites Not In This Site Link list, select the sites you wish to associate with this link and click Add. They will appear on the right side of the dialog box under Sites In This Site Link. Click OK to complete the link creation.
+   5. Right-click the site link you just created and select Properties. The site link cost is set to 100 by default; modify this number, if necessary, according to your site link plan. Remember that a lower number indicates a preferred path.
+   6. If you wish to change the replication frequency to something other than the default of 180, modify the Replicate Every xx Minutes field.
+   7. To modify the schedule to allow replication to take place only during the hours you specify, click Change Schedule.
+   8. Select the days and hours you wish to disallow or allow replication and adjust the option button to the right of the schedule chart to show the appropriate color. Days and hours highlighted in blue indicate that replication is allowed. When finished, select OK to close the Schedule dialog box.
+   9. Upon completing all desired link configurations, click OK.

PAUSE. LEAVE the Sites and Services MMC snap-in open to complete the next exercise.

When designing your site link topology, the values that you assign to these attributes must be considered carefully for maximum replication performance. Use the following guidelines when setting link properties:

+   • Cost attribute values should consider the speed and reliability of the links in use. For example, you would assign a relatively lower cost to a reliable T-1 link than to a 128-Kbps ISDN link that is only utilized when the T-1 is unavailable.
+   • Schedule attribute values should consider the tradeoff between replicating during off-peak hours and having the most up-to-date information at all sites.
+   • Short frequency attribute values consume less bandwidth due to frequent small replication cycles, as well as providing more up-to-date information. Longer replication intervals may require more bandwidth during replication and less up-to-date information between replication cycles.

# Selecting a Replication Protocol

When configuring replication, you can choose between two possible protocols: RPC over IP and SMTP. In this section, we'll discuss the differences between these two replication protocols. We will also look at situations in which you might choose one over the other, based on the advantages and disadvantages of each.

> TAKE NOTE
> After you have created a site or a site link object, you can go to the Properties sheet for that object and place a checkmark next to Protect from Accidental Deletion on the Object tab. As the name implies, this will protect you against an administrator deleting a critical object, like a site, by mistake; with this checkbox selected, Active Directory will not allow the deletion and will instead raise an error message alerting the administrator that the object has been protected against deletion.
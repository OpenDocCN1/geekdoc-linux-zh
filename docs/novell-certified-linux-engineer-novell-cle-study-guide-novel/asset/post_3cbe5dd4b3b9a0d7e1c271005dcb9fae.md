
# CHAPTER 7 Synchronizing User Identities with DirXML

**FIGURE 7.17** Schema-mapping rule.

c. Review the default attribute mappings and then select **Cancel**, **Cancel**.

24. View the placement rule on the publisher channel by completing the following steps:

a. On the publisher channel, click the **Placement Rule** icon.

b. In the **DirXML Rule** drop-down list, select **Edit XML**. The screen shown in Figure 7.18 is displayed.

![](img/c7771e8540507f2b00c088c7a411b57b_321_1.png)

**FIGURE 7.18** Placement rule.

c. Notice that users from the CSV text files are placed in the **DirXMLUsers.IF.CLE** container.

d. Click **Cancel**.

25. Repeat these steps to view the event and output transformation stylesheets on the subscriber channel as well as the import transformation, matching, and creation rules on the publisher channel. Be sure you don't change any of the default parameters.

26. Start the driver by selecting the red circle with the minus sign icon; then click **Start Driver**.

27. Wait while the driver starts.

At this point, the driver should start and you're ready to move to Lab Exercise 7.2.

## Lab Exercise 7.2: Testing the DirXML Delimited Text Driver

The Delimited Text driver includes a sample CSV file that we're going to use to test the implementation.

To do this, complete the following steps:

1. At the shell prompt, enter `cp /usr/lib/dirxml/rules/delim/sample.csv /tmp/DirXML/Input`.

2. Remember that the publisher channel polls the configured input directory every 10 seconds. Wait this amount of time and then check to see that the information was synchronized by completing these steps:

   a. Under **eDirectory Administration** in iManager, select **Modify Object**.

   b. Click the **Browse** icon.

   c. Select **Browse**.

   d. Browse to the **DirXMLUsers.IF.CLE** container. You should see a large number of new users added by the Delimited Text driver.

   e. Select **Cancel**, **Cancel**.

The next thing we need to do is export data from the eDirectory tree to a CSV file in the output directory. Complete the following steps:

1. In iManager, select the **Overview** task under the **DirXML Management** role.

2. Mark **Search Entire Tree** and then click **Search**.

3. In the **DirXML Overview** screen, click the **Text Delimited** icon.

4. Scroll to the bottom of the page and select **Migrate from eDirectory**. The screen in Figure 7.19 is displayed.

5. Click **Add**.

**FIGURE 7.19** Migrating users from eDirectory.

![](img/c7771e8540507f2b00c088c7a411b57b_323_0.png)

6. Browse to and select the first user in the **SLC.CLE** container in your tree.

7. Repeat this process to add all the users in the **SLC.CLE** container.

8. Click **OK**.

9. When prompted that the migration was started, click **OK**.

10. At the shell prompt, enter `cd /tmp/DirXML/Output`.

11. Enter `ls -1`. You should see a CSV file listed with a random number for a file name.

12. View the contents of the file by entering `cat ./file_name.csv` or `more`. You should see an entry for each user you specified for migration from the tree.

13. Stop the Delimited Text driver by clicking the yin-yang icon in the **Driver Overview** screen in iManager.

14. Click **Stop Driver**.

Congratulations! You just configured your first DirXML driver. The Delimited Text driver is relatively simple compared to the other DirXML drivers. Let's ratchet things up a bit and look at how to synchronize two eDirectory trees using DirXML.

## Installing and Configuring the DirXML eDirectory Driver

Test Objective Covered:

- 5. Implement the eDirectory driver for DirXML.

The DirXML eDirectory driver is a very useful tool. Consider the following hypothetical (although quite common) situation: Suppose ABC, Inc. purchases a smaller company and both companies have their own eDirectory trees populated with network information.

What would the network administrators need to do in order to manage the disparate trees? Prior to DirXML, there were three options:

- Do nothing and maintain separate trees. This isn’t a good solution. To provide users in each tree access to network resources, they must maintain duplicate sets of accounts in each tree.
- Re-create data from one tree in the main tree. This can be done manually or by using LDIF export files. Either way, this represents a sizeable task.
- Merge the trees. Two eDirectory trees can be merged together. However, this can be a difficult and dangerous endeavor (ask anyone who has done it in a production environment).

DirXML offers a fourth option that is easier and safer than the others. Using the eDirectory driver, the ABC, Inc. administrator can synchronize data between the trees. He can configure one tree to be the authoritative data source, sending but not receiving updates. He can configure the other tree to be a data consumer, receiving but not sending updates.

Alternatively, he can configure a bidirectional system where changes in either tree are immediately synchronized to the other. Whichever approach is selected, this is done the same as with other DirXML drivers, by implementing publisher and subscriber channel filters.

This driver can be a useful tool in a variety of circumstances, including situations such as company acquisitions (mentioned earlier) and consolidating a multi-tree organization. It can also be implemented in situations where an organization has deployed an LDAP-compliant application that expects all directory information to reside in a single container (this happens frequently).

Using the eDirectory driver, you can configure a second tree in your organization and synchronize all directory data from your production tree (which is hierarchical) to the secondary tree (which is flat).

### About the DirXML eDirectory Driver

The eDirectory driver is unique among the various DirXML drivers. With most drivers, there is a driver installed for the third-party database. Only one instance of DirXML is installed and configured, as shown in Figure 7.20.

![](img/c7771e8540507f2b00c088c7a411b57b_325_0.png)

When you're using the eDirectory driver, however, things are a little bit different. First of all, DirXML is installed on both servers that have trees to be synchronized. Second, an eDirectory driver is configured on both servers, as shown in Figure 7.21.

![](img/c7771e8540507f2b00c088c7a411b57b_326_0.png)

**FIGURE 7.21** Using DirXML with eDirectory.

Another (third) difference is in the way the publisher and subscriber channels are configured. To understand this, let's use the analogy of how to make a null modem cable out of a serial cable. All you have to do is rewire the cable plug such that the Tx (transmit) wire in the cable connects to the Rx (receive) wire in the serial port plug on the PC. Configured this way, transmitted data is sent from the Tx wire to the Rx wire in the port, and vice versa.

Essentially, you have the same situation with the DirXML eDirectory driver. Because you have two drivers and two DirXML engines, you have two publisher channels and two subscriber channels.

The eDirectory drivers are configured such that the publisher channel in one tree is connected to the subscriber channel in the other, and vice versa. This is depicted in Figure 7.21.

This can complicate things a bit for the NNLS implementer. It means that information travels first through the first tree’s subscriber filter—having all its rules and filters applied—and then through the other tree’s publisher channel—having all its rules and filters applied.

Having set this kind of implementation up several times, I can tell you that if you can keep this one point in mind, it will make configuring the eDirectory driver much easier for you. My experience has been that it is very easy to think from the standpoint of one tree or the other, but not both at the same time. By forgetting that the subscriber channel becomes the publisher channel, and vice versa, you can potentially make grievous mistakes when configuring your drivers.

You also need to be concerned with object placement. With most other DirXML drivers (with the exception of the Active Directory driver), data is being synchronized with a flat-file database. Object placement in this situation is rather easy. If you’re good with the XML markup language, you can even customize your placement rule such that placement is based on a particular attribute.

For example, you can configure the rule such that if the PeopleSoft database shows an employee’s address to be in Idaho Falls, Idaho, DirXML automatically creates the associated user object in the IF.CLE container. If the employee’s address is in Salt Lake City, Utah, on the other hand, the object is created in the SLC.CLE container.

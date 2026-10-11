
14. Review the default publisher and subscriber channel rules by completing the following steps:
- a. On the publisher channel, select the Creation Rule icon.
- b. In the DirXML Rule drop-down list, select Edit XML. Notice that user objects must have the Given Name and Surname attributes populated in order for them to be created in the tree.
- c. Click Cancel.
- d. On the publisher channel, select the Placement Rule icon.
- e. In the DirXML Rule drop-down list, select Edit XML. Notice that users will be placed in RemoteUsers.IFCLE and groups will be placed in RemoteGroups.IFCLE.
- f. Click Cancel.
- g. On the publisher channel, select the Matching Rule icon.
- h. In the DirXML Rule drop-down list, select Edit XML. Notice that users will be matched on the CN, Given Name, and Surname attributes. Also, notice that groups will be matched only on the CN attribute.
- i. Click Cancel.
- j. In the Driver Overview screen, notice that the input transformation rule, schema-mapping rule, event transformation rule, and the command transformation rule are all blank. Because we're synchronizing two similar databases, these aren't needed.
- k. Also in the Driver Overview screen, notice that none of the subscribe channel rules are populated. Because the subscriber channel is connected to the publisher channel on the other system, the rules on the remote publisher channel will be used to configure data.

15. Configure the eDirectory driver on CLE2 by completing the following steps:
- a. Run a web browser and open iManager by navigating to `https://your_CLE2_server_IP_address/nps/iManager.html`.
- b. Authenticate as **admin** with a password of **novell**.
- c. Under the **DirXML Management** role, select the **Create Driver** task.
- d. In the **Create Driver Welcome** screen, select **In a new driver set** and then click **Next**.
- e. In the **Name** field, enter `CLE2DriverSet`.
- f. In the **Context** field, enter `CLE.ANNAPOLIS`.
- g. In the **Server** field, enter `CLE2.CLE.ANNAPOLIS` and then click **Next**.
- h. In the **Import a pre-configured driver from the server (.XML file)** drop-down list, select **eDir-Driver.xml** and then click **Next**.
- i. In the **Driver Name** field, enter **eDir-Driver**.
- j. In the **Remote Tree Address** and **Port** fields, enter the IP address of your CLE1 server. Be sure **8196** is entered in the **Port** field.
- k. In the **Configure Data Flow** drop-down list, select **Bidirectional**.
- l. In the **Configuration Option** drop-down list, select **Flat**.
- m. In the **Base Container** field for users, enter **RemoteUsers.CLE.ANNAPOLIS**.
- n. In the **Group Container** field, enter **RemoteGroups.CLE.ANNAPOLIS**.
- o. Click **Next**.
- p. Select **Define Security Equivalences**.
- q. Click **Add**.
- r. Browse to and select `admin.CLE.ANNAPOLIS` and then click **OK**.
- s. Select **Exclude Administrative Roles**.
- t. Click **Add**.
- u. Browse to and select `admin.CLE.ANNAPOLIS` and then click **OK**.
- v. Click **Next**.
- w. In the **Summary** screen, click **Finish with Overview**.

16. Configure the filters in the CLE2-Tree by completing the following steps:
- a. In iManager, view the **Driver Overview** screen by selecting the **eDirectory** icon.
  > Don't select the red minus sign, which is used to start and stop the driver.
- b. On the subscriber channel, select the **Subscriber Filter** icon.
- c. Select **For All Classes** in the Filter.
- d. In the right column, *deselect* the **ACL** attribute and then click **OK**.
- e. Click **OK**.
- f. On the publisher channel, select the **Publisher Filter** icon.
- g. Select **For All Classes** in the Filter.
- h. In the right column, *deselect* the **ACL** attribute and then click **OK**.
- i. Click **OK**.

17. Start the eDirectory driver on both servers by completing the following steps:
- a. Open a second browser window and open `https://your_CLE1_server_IP_address/nps/iManager.html`.
- b. Authenticate as **admin** with a password of **novell**.
- c. Under **DirXML Management**, select **Overview** and then select **Search**.
- d. Select the **eDirectory driver** icon in the **CLEDriverSet2** driver set.
- e. You should now have two browser windows, one with the CLE1 Driver overview displayed, and the other with the CLE2 Driver overview displayed.
- f. In each window, select the red minus sign and then select **Start Driver**.

> If you experience problems with starting the driver, you may need to restart the ndsd daemon. Do this by entering `/etc/init.d/ndsd stop` and then `/etc/init.d/ndsd start`. Then refresh the Overview screen.
>
> TIP

18. Check the state of the synchronization by completing the following steps:
- a. In both trees, use the **Modify Object** task under **eDirectory Administration** to browse the contents of the **RemoteUsers** containers.
- b. Notice that they are empty. The eDirectory driver is *event driven*. Without an event, no synchronization occurs.
- c. Click **Cancel**.

19. Manually migrate users by completing the following steps:
- a. In the CLE2 iManager browser window, select the **Overview** task under the **DirXML Management** role.
- b. Click **Search**.
- c. Select the **eDirectory** driver icon.
- d. Scroll down to the bottom of the page and select **Migrate from eDirectory**.
- e. In the **Migrate Data** screen, click **Add**.
- f. Browse to **CLE.ANNAPOLIS** and select **Jastin**.
- g. Repeat this to add the rest of the users, except for **admin**, **eGuidePublicUser**, and **iFolder_ServiceAgent**, in the CLE container.
- h. Click **OK**.
- i. When prompted that the migration was started, click **OK**.
- j. Wait while the users are migrated.
- k. When the migration is complete, click **OK**.
- l. Switch to your **CLE1 iManager** browser window.
- m. Use the **Modify Object** task under the **eDirectory Administration** role to browse the contents of the **RemoteUsers.IFCLE** container. You should see all the users you migrated from the remote tree.
- n. Select **Cancel**, **Cancel**.
- o. In the **CLE1 iManager** browser window, repeat the preceding steps to migrate all users in the IFCLE container, except for **admin**, **eGuidePublicUser**, and **iFolder_ServiceAgent**, to the **CLE2-Tree**.
- p. Switch back to the **CLE2 iManager** browser window.
- q. Use the **Modify Object** task under the **eDirectory Administration** role to browse the contents of the **RemoteUsers.CLE.ANNAPOLIS** container. You should see all the users you migrated from the remote tree.

20. Recall that the matching rule establishes associations between objects in the connected systems. Changes made to one object should be synchronized to its associated object in the other tree. Test synchronization by completing the following steps:
- a. In the CLE2 iManager browser window, use the **Modify Object** task to change the title of the **KLarsen.CLE.ANNAPOLIS** user object to **Assistant Director**.
- b. In the CLE1 iManager browser window, use the **Modify Object** task to verify that the title of the **KLarsen.RemoteUsers.IFCLE** user was changed to **Assistant Director**.

21. eDirectory synchronization is working! Before ending this exercise, shut down your DirXML drivers on both servers by completing the following steps:
- a. In your CLE1 iManager browser window, select **Overview** under **DirXML Management**.
- b. Select **Search**.
- c. Click the **yin-yang** icon for the eDirectory driver and then select **Stop Driver**.
- d. Switch to your CLE2 iManager window and repeat these steps to shut down the eDirectory driver on CLE2.
- e. In the eDirectory driver overview, select the **eDirectory Driver** icon.
- f. In the drop-down menu, select **Driver Configuration**.
- g. Scroll down to the **Startup** options and select **Disabled**.
- h. Click **OK**.

Congratulations! You have just successfully configured and implemented the most difficult component of NNLS. Although difficult to learn, once you get the hang of DirXML, the possibilities are immense.

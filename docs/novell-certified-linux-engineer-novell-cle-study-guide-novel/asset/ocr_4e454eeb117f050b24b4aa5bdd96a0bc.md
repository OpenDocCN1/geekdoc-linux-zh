+   e. In the **Name** field, enter `CLE2DriverSet`.

+   f. In the **Context** field, enter `CLE.ANNAPOLIS`.

+   g. In the **Server** field, enter `CLE2.CLE.ANNAPOLIS` and then click **Next**.

+   h. In the **Import a pre-configured driver from the server (.XML file)** drop-down list, select **eDir-Driver.xml** and then click **Next**.

+   i. In the **Driver Name** field, enter **eDir-Driver**.

+   j. In the **Remote Tree Address** and **Port** fields, enter the IP address of your CLE1 server. Be sure **8196** is entered in the **Port** field.

+   k. In the **Configure Data Flow** drop-down list, select **Bidirectional**.

+   l. In the **Configuration Option** drop-down list, select **Flat**.

+   m. In the **Base Container** field for users, enter **RemoteUsers.CLE.ANNAPOLIS**.

+   n. In the **Group Container** field, enter **RemoteGroups.CLE.ANNAPOLIS**.

+   o. Click **Next**.

+   p. Select **Define Security Equivalences**.

+   q. Click **Add**.

+   r. Browse to and select `admin.CLE.ANNAPOLIS` and then click **OK**.

+   s. Select **Exclude Administrative Roles**.

+   t. Click **Add**.

+   u. Browse to and select `admin.CLE.ANNAPOLIS` and then click **OK**.

+   v. Click **Next**.

+   w. In the **Summary** screen, click **Finish with Overview**.

16. Configure the filters in the CLE2-Tree by completing the following steps:

+   a. In iManager, view the **Driver Overview** screen by selecting the **eDirectory** icon.

> Don't select the red minus sign, which is used to start and stop the driver.
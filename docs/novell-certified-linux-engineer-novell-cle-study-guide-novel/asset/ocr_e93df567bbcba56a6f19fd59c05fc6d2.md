+   I. In the **Configuration Option** drop-down list, select **Flat**.

+   m. In the **Base Container** field for users, enter **RemoteUsers.IFCLE**.

+   n. In the **Group Container** field, enter **RemoteGroups.IFCLE**.

**WARNING**  In steps **m** and **n**, don't use the **Browse** button. It causes problems!

+   o. Click **Next**.

+   p. Select **Define Security Equivalences**.

+   q. Click **Add**.

+   r. Browse to and select **admin.IFCLE** and then click **OK**.

+   s. Select **Exclude Administrative Roles**.

+   t. Click **Add**.

+   u. Browse to and select **admin.IFCLE** and then click **OK**.

+   v. Click **Next**.

+   w. In the **Summary** screen, click **Finish with Overview**.

+   13. Configure the filters in the **CLE1-Tree** by completing the following steps:

+   a. In **iManager**, view the **Driver Overview** screen by selecting the **eDirectory** icon.

**WARNING**  Don't select the red minus sign, which is used to start and stop the driver.

+   b. On the **subscriber** channel, select the **Subscriber Filter** icon. The attributes displayed are those that are allowed through the filter.

+   c. Notice that the **Access Control List (ACL)** attribute is allowed through the filter. This should be removed. Most ACLs contain tree-specific information that can cause synchronization problems. Select **For All Classes** in the **Filter**.

+   d. In the right column, deselect the **ACL** attribute and then click **OK**.

+   e. Click **OK**.

+   f. On the **publisher** channel, select the **Publisher Filter** icon.

+   g. Notice that the **ACL** attribute is also allowed through on the publisher channel. Repeat the preceding steps to remove this attribute.
+   19. Manually migrate users by completing the following steps:
+   
+   a. In the CLE2 iManager browser window, select the **Overview** task under the **DirXML Management** role.
+   
+   b. Click **Search**.
+   
+   c. Select the **eDirectory** driver icon.
+   
+   d. Scroll down to the bottom of the page and select **Migrate from eDirectory**.
+   
+   e. In the **Migrate Data** screen, click **Add**.
+   
+   f. Browse to **CLE.ANNAPOLIS** and select **Jastin**.
+   
+   g. Repeat this to add the rest of the users, except for **admin**, **eGuidePublicUser**, and **iFolder_ServiceAgent**, in the CLE container.
+   
+   h. Click **OK**.
+   
+   i. When prompted that the migration was started, click **OK**.
+   
+   j. Wait while the users are migrated.
+   
+   k. When the migration is complete, click **OK**.
+   
+   l. Switch to your **CLE1 iManager** browser window.
+   
+   m. Use the **Modify Object** task under the **eDirectory Administration** role to browse the contents of the **RemoteUsers.IFCLE** container. You should see all the users you migrated from the remote tree.
+   
+   n. Select **Cancel**, **Cancel**.
+   
+   o. In the **CLE1 iManager** browser window, repeat the preceding steps to migrate all users in the IFCLE container, except for **admin**, **eGuidePublicUser**, and **iFolder_ServiceAgent**, to the **CLE2-Tree**.
+   
+   p. Switch back to the **CLE2 iManager** browser window.
+   
+   q. Use the **Modify Object** task under the **eDirectory Administration** role to browse the contents of the **RemoteUsers.CLE.ANNAPOLIS** container. You should see all the users you migrated from the remote tree.

+   20. Recall that the matching rule establishes associations between objects in the connected systems. Changes made to one object should be synchronized to its associated object in the other tree. Test synchronization by completing the following steps:
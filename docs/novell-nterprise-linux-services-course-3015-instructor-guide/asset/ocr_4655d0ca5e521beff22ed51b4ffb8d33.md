# Exercise 6-1  Confirm the iFolder 2.1 Installation on Your NNLS Server

**10 minutes**

In this exercise, you confirm that iFolder is installed on your NNLS server. (iFolder was installed in Exercise 2-1.)

Do the following:

+   1. Check your **DAX-TREE** to make sure that the iFolder objects have been created:
+       a. From your NNLS server desktop, launch **Mozilla**; then start iManager by entering the following:
+           https://DAX.your_container.Digita1AirIines.com /nps/iManager
+       b. Log in as **admin** with a password of **novell**.
+       c. At the left under **eDirectory Administration**, select **Modify Object**; then select the **Object Selector** icon (magnifying glass) on the right.
+       d. Select **Browse**.
+       e. Browse to and view the contents of **your container**.
+          You might need to select **Next** to view the iFolder objects. You should see the following:
+          - iFolder_ServerAgent (this has a user icon)
+          - iFolder_Settings
+          - iFolder_ldap01
+          - iFolder_server01
+       f. Select **iFolder_Settings**; then select **OK**.
+          Note the valued attributes and the unvalued attributes that can be added to the Valued Attributes list.
+       g. Select **Cancel**.

If students inadvertently accessed this object through the iFolder Server Management link, they will not be able to open this object.
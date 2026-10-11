+   4.  Under **Linux User Management**, select **Convert eDirectory User to LUM User**.  
+   5.  In the **Select User** field, browse to and select the user you want to convert.  
+   6.  Click **OK**. The screen in Figure 8.39 appears.

![](bbox=[0.08, 0.19, 0.71, 0.46])

# **FIGURE 8.39**  
Converting an existing user to a Samba user.

+   7.  In the **Enter the Primary Group for this User** field, browse to and select the LUM-enabled group the given user is a member of.  
+   8.  Make sure the **Also convert this User object to a Samba User object** box is marked.  
+   9.  In the **Enter the desired Samba password** field, enter the Samba password for the user. As mentioned before, you should consider using the user’s eDirectory password for the Samba password. Otherwise, the user will have to remember two passwords—one to authenticate to the tree and one to access Samba resources.  
+   10. Click **OK**.  
+   11. When prompted that the process was successful, click **OK**. If you have more users to convert, you could select **Repeat Task** to repeat this process on the rest of the user objects.

NNLS also includes a version of the smbpsswd utility that you may be familiar with if you’ve implemented the non-NNLS version of Samba. You can use this utility to set the Samba password for a user object. However, it doesn’t convert the user to a LUM/Samba user, nor does it configure LUM attributes. Novell recommends that you use iManager to configure your Samba users instead.
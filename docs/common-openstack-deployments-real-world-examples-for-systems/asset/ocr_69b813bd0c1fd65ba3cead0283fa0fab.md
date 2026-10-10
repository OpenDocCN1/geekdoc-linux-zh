+   • **System Information**: See an overview of what is currently enabled in your DevStack instance.

Next you'll want to explore the Identity Panel, which has the following:

+   • **Projects**: An organizational unit in the OpenStack cloud that may be shared between users with varying permissions. By default, each user comes with a single project that only they belong to.
+   • **Users**: Allows you to manipulate the users that exist on the system. Note that some of these users are system users (such as the ones that control Glance and Nova) and are required for the operation of OpenStack. These system users should not be deleted. Also be mindful that care should be taken in changing passwords while running DevStack, since some of these are hard-coded in configuration files.
+   • **Groups**: A collection of users who are assigned to a specific project or domain.
+   • **Roles**: A defined series of permitted actions that you can assign to a specific project or domain.

You can learn more about using Horizon in Chapter 6, “Private Compute Cloud.”

![](bbox=[0.1, 0.47, 0.85, 0.9])
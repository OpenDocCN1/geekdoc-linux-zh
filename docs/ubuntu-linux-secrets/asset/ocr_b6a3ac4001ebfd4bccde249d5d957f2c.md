![](bbox=[0.205, 0.195, 0.615, 0.505])

Figure 17-6: Delete User dialog box.

# Ubuntu Groups

Individual user accounts are great for keeping documents and folders private on the Ubuntu workstation, but they are not at all useful for sharing documents and folders. Sharing documents is a common practice in many work environments.

The Ubuntu system provides another privilege level that facilitates sharing documents and folders. Groups are a collection of user accounts that have a privilege requirement in common. For example, you can create a group called "sales" that has read and write privileges to a folder specifically used for the sales team. Any user account that's a member of the sales group will have full access to any document in that folder.

Individual users can be members of more than one group, although only one group is considered the main group for the user account. The main group is what Ubuntu uses to assign group privileges on any files or folders a particular user creates. By default, Ubuntu creates a separate group for each user account to use as the main group. To keep things simple, Ubuntu names the user's group the same as the user account username.

The Ubuntu workstation comes with lots of groups already configured in the system. If you look at the groups, some of them should look similar to the options available in the User Privileges tab when you add a new user (see the "Adding Users" section earlier in this chapter).

Ubuntu creates special groups to control access to features on the system, such as administering the system and using specific hardware devices. To allow a user access to these features, Ubuntu assigns the user account to the appropriate group.

Besides these groups, Ubuntu also creates groups to be used by specific applications and services running on the system. Table 17-1 describes these groups.

All of the special groups have group ID values lower than 1,000, allowing Ubuntu to easily separate the special groups from the user groups. You can manage any of the groups on the system, but it's a good idea not to mess with the special groups unless you know what you're doing. Otherwise, the related services may break!
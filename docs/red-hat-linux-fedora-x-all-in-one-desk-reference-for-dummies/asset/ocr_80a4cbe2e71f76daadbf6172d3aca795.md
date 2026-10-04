# Adding User Accounts

When you start Fedora Core for the first time, you get the chance to add a personal user account. If you didn't add a user account during the first boot as described in Chapter 4 of this minibook (or if you want to add more user accounts for family members or coworkers), you can do so at any time using the Red Hat User Manager.

Setting a personal user account other than root is a good idea. The problem with root is the absolute power of superaccount — you can literally do anything, except destroy critical systems, with ease. As an ordinary user is better. When you must do something as root, simply type the su command. When you're prompted for the root password and after you enter that, you become root. When you finish with your super duties, type exit to return to your mortal self.

To add user accounts with the User Manager, follow these steps:

+   Choose Main Menu:System Settings→Users and Groups from the GNOME desktop.

If you're not logged in as root, the User Manager prompts you for the root password (see Figure 3-6), which you have to enter to run the manager.

![](bbox=[0.135, 0.555, 0.515, 0.668])

Enter the password and click OK.

The User Manager window (shown in Figure 3-7) features two tabs: Users and Groups. The Users tab displays the current list of user accounts. The Groups tab lists your current groups. Figure 3-7, for example, lists the users on my Fedora Core system; the list is different on your system.

+   To add a new user, click the Add User button on the toolbar.

The Create New User dialog box appears, as shown in Figure 3-8.
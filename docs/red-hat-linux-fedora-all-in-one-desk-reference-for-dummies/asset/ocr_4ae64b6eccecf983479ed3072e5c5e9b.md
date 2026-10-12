# Adding User Accounts

Figure 3-6:
The sound card configuration utility displays information about the sound card.

![](bbox=[0.22, 0.16, 0.48, 0.42])

When you start Red Hat Linux for the first time, you get the chance to add a personal user account. If you didn't add a user account during the first boot as described in Chapter 4 of this mini-book (or if you want to add more user accounts for family members or coworkers), you can do so at any time by using the Red Hat User Manager.

![](bbox=[0.15, 0.64, 0.22, 0.77])

Setting up a personal user account other than root is a good idea. The problem with root is the absolute power of that superuser account — you can literally do anything, even destroy critical system files, with ease. It's better to log in as an ordinary user. When you must do something as root, simply type the su command. You'll be prompted for the root password; after you enter that password you'll become root. When you're finished with your superuser duties, type exit to return to your mere mortal self.

To add user accounts with the Red Hat User Manager, follow these steps:

+   1. Choose Main Menu→System Settings→Users and Groups from the GNOME desktop.

If you're not logged in as root, the Red Hat User Manager prompts you for the root password (see Figure 3-7), which you have to enter to run the manager.

Figure 3-7:
Enter the root password here.

![](bbox=[0.25, 0.81, 0.52, 0.92])
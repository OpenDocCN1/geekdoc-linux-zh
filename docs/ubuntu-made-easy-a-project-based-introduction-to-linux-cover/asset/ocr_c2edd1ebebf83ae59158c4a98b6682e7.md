![](bbox=[0.23955, 0.06935, 0.86045, 0.35645])

# # Project 18B: Installing Parental Controls

One major concern of most parents is how long their children are spending on the computer. Most systems provide parents with a way to monitor this through parental control settings. There are a couple of parental control packages for Ubuntu. One, called Nanny, is in the Ubuntu Software Center but does not work with the new Ubuntu 12.04 release. Another, timeprk can work after a bit of trickery at the command line but is not included in the Ubuntu Software Center. Nanny is useful in that it allows you to control web access, since we want something that will work, we'll settle for timeprk now and just hope that Nanny is fixed in the near future (keeping checking).

Before you use timeprk, you will need to have separate (not administrator) accounts for your kids; otherwise, timeprk will not work. If you have not created user accounts for the kids, do that first (Chapter 9 if you need a review).

Once you've done, you can move on to the first part of the project: creating a symbolic link that diverts timeprk from the support file it needs is looking for (called GDM), which is no longer in Ubuntu, to another support file that is essentially the same thing, albeit with another name (LDM), and is in Ubuntu. This is necessary because the version of timeprk we will be installing was prepared for the previous version of Ubuntu (Unity Ocelot). But don't worry, the fix works, and it's not difficult. Here are the steps:

+   1. Open the Terminal (from the Dash, type **terminal and press ENTER**).
2. Create the symbolic link by typing `sudo ln -s /etc/mdm/etc/gdm` and pressing ENTER. Type your password when prompted and then press ENTER.
3. You can now close the Terminal.
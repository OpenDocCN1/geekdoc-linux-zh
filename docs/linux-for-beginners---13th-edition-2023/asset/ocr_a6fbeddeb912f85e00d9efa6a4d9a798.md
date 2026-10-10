# # Install Apps via the Terminal – Part 1

There are different ways to install apps and programs on Linux. You can opt for the graphical route, using a Software Manager, or you can use the Terminal. Often, the Terminal provides better control over the software being installed and sometimes, you have no choice in the matter.

# ## COMMAND LINE INSTALLS

Installing an app with the Terminal may require some nifty keyboard work but you get a better sense of what's being installed and where.

# **STEP 1**

Installing apps form the Terminal is often relatively simple. First though, you need to make sure that the system is up to date. To do this open up the Terminal and enter: sudo apt-get update && sudo apt-get upgrade. Enter your password and accept any necessary updates.

# **STEP 3**

You need to enter y to confirm the installation, which takes up around 5.5MB of storage in the system. Once Stella is installed, you can see again that Mint has automatically created the Games category in the Menu as well as the app shortcut.

![](bbox=[0.07, 0.55, 0.48, 0.68])

![](bbox=[0.53, 0.55, 0.92, 0.68])

# **STEP 2**

Just as you've seen, sudo apt-get update/upgrade and so on are designed to upgrade the software that's already installed on the system. How do you install more apps though? It just so happens that it's extraordinarily simple. First you need an app to install, so let's use Stella again. Enter: sudo apt-get install stella.

# **STEP 4**

Sometimes, when installing software, you need to add the app's Repository. The repository, or repo, is simply the remote server location where the software is held, along with all its dependencies (the vital libraries and such it needs to function). Start by typing in this: sudo add-repository ppa:peterlev1/ppa. Press Enter when asked to and add the PPA (Personal Package Archive).

![](bbox=[0.07, 0.82, 0.48, 0.95])

![](bbox=[0.53, 0.82, 0.92, 0.95])
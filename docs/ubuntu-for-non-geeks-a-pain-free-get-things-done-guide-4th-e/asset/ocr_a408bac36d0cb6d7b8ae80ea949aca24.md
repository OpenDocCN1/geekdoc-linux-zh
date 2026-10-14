# Software Installation Problems

Ubuntu’s software management tools tend to operate pretty smoothly these days. Nevertheless, I’ve included some troubleshooting tips for two or three problems that used to be common (but seem to be getting rarer with each release). If you’re having a problem with installing, removing, or updating packages, this section is for you.

# I Get an Error About Unauthenticated Packages

If you get an error message about unauthenticated packages when you try to install a program, try the following:

+   1. Select System ▸ Administration ▸ Update Manager to open the Update Manager.
+   2. Click the Check button, and enter your password if prompted. The package list will be updated, along with all the files that are used to check whether your packages are "authentic."
+   3. When it has finished updating the package list, close the Update Manager, and try to install your program again.

If you’re still getting the error message, you may have added a software repository without adding its GPG key. The GPG key is required to do the authentication stuff that the error message is talking about. If this is the case, look at "Adding Extra Software Repositories" on page 86 for instructions on how to add the GPG key for a repository.

# I Get a dpkg Error

There are a couple of common reasons why you might get an error message related to dpkg when you try to install, update, or remove a software package.

If you get an error saying E: Sub-process /usr/bin/dpkg returned an error code (1), you could have a broken package on your system. Here are some techniques you can try to fix a broken package:

+   1. Select Application ▸ Accessories ▸ Terminal to open a Terminal.
+   2. Type sudo apt-get install --fix-broken, and press ENTER. Type your password when prompted, and press ENTER again. This command looks for broken packages and tries to fix them.
+   3. With any luck, this will fix the problem; try installing a package via the Ubuntu Software Center to see whether you still get the dpkg error message.
+   4. If you do still get the error message, type sudo dpkg --configure -a into the Terminal, and press ENTER. This command tries to fix half-installed packages if there are any.
+   5. Try installing a package from the Ubuntu Software Center again. If you’re still getting an error message, ask for help on the Ubuntu forums.
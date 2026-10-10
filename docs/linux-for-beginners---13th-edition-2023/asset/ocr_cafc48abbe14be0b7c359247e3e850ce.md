# Install Apps via the Terminal – Part 2

STEP 5
If you enter `ls` again, you'll notice that a new folder has been created: `vim74`; in light blue text representing a folder in Min. It's always handy to create root folders for the main app, then as you upgrade apps through this method the individual versions will each have their own folder.

![](bbox=[0.07, 0.22, 0.48, 0.38])

STEP 6
Type in `cd vim74` to enter the folder, and `ls` again to view its contents. There will likely be a fair number of files present; most are the app’s core files, while others will be labelled `README` or `INSTALL`. It’s always wise to read these files first as they provide valuable information regarding the installation.

![](bbox=[0.07, 0.5, 0.48, 0.67])

STEP 7
The first part of the installation requires you to enter `./configure`. The `./configure` command will check your system for any missing dependencies associated with the app. If you received an error regarding a C Compiler, then enter: `sudo apt-get install build-essential`. The third-party app Ncurses was recorded as missing. So we need to install that with `sudo apt-get install libncurses5-dev libncursesw5-dev`.

![](bbox=[0.07, 0.8, 0.48, 0.97])

STEP 8
You may need to keep installing new dependencies, depending on the app. After each new dependency is installed, re-run `./configure` and when it doesn’t report back with an error you can continue to the next stage of the installation. Note: you may need to search online for some error messages.

![](bbox=[0.52, 0.22, 0.94, 0.38])

STEP 9
With a successful `./configure`, the system will create a `Makefile`. This needs to be ‘made’ by entering `make` into the Terminal. This may take a while, depending on the size of the app.

![](bbox=[0.52, 0.5, 0.94, 0.67])

STEP 10
Finally, you need to enter: `sudo make install` into the Terminal. This will install the app, and make it ready for use in the system. When complete you can execute the app, in this case by entering `vim` into the Terminal or searching for it via the Dash.

![](bbox=[0.52, 0.8, 0.94, 0.97])
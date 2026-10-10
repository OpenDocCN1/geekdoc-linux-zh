# ## Setting Up a Graphical Login Screen

Admit it — part of the reason you installed KDE in the first place was that you simply find the graphical interface more pleasing than plain old white text on black background. So maybe it bugs you that you have to exit KDE and go back out to the text prompt after you're done with your session, leaving your computer to look like any other UNIX-type machine with its simple little `login: prompt` sitting there quietly.

The solution is to create a graphical login screen. After you have it set up, you never need to stop running KDE if you don't want to. Go ahead and log out as you normally do. Instead of exiting KDE, though, your computer returns to a graphical login screen — but KDE is still going! No more typing `startx` after logging in, no more waiting for the desktop to appear.

![](bbox=[0.1, 0.4, 0.2, 0.48])

We have to apologize to you, gentle reader. Normally, we stick in a couple of pictures to show you exactly what the graphical login screen looks like. In fact, we take screenshots, exactly as we describe the process in Chapter 11. Unfortunately, in order to take a screenshot, we have to be logged into the computer so that we can use KSnapshot. Do you begin to see the problem? We can't get the login screen on the monitor until we log out — but we can't take a screenshot until we're logged in. So, you have to trust us that this works: give it a try to see what your login screen looks like. If you don't like it, you can always turn the screen off (We did include some illustration of screens you use in setting up the graphical screen.)

![](bbox=[0.1, 0.59, 0.2, 0.67])

You must log in as root to create a graphical login. You do not need to log in as root to use the graphical login; everyone with user accounts on your machine sees the graphical login screen after you set it up.

Here's how you set up a graphical login screen:

+   1.  **Log in as root.**
+       If you have to log out of your user account and back in as root, do so now.

+   2.  **Open the KDE menu and choose `Settings::Applications::Login Manager`.**
+       The Login Manager screen (\"KDM Configuration\") appears, as seen in Figure 14-1.

+   3.  **Click the Appearance tab.**
+       This should be the default; if it isn't, just click it now.
+       The Appearance tab contains a whole slew of options for you to choose from. You can decide whether to use a greeting message, a logo, or one of several \"GUI styles\" that set the overall look of the screen. Make your selections on this tab.
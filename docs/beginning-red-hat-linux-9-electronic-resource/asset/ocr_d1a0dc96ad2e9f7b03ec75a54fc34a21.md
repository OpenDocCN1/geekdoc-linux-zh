+   3. Now, back in the **Edit Profiles** window, select the **root** profile and press the **Edit** button. Now you can use your creativity to personalize the window used for root shells. For example, you can change window title to **root shell**, and set the color scheme to white-on-red, as shown below:

![](bbox=[0.07, 0.15, 0.96, 0.46])

Whatever you decide to do, you *must* select the **Run a custom command instead of my shell** checkbox in the **Title and Command** tab, and the command *must* be `su -`. It is this that ensures that, whenever this profile is activated in the terminal, Linux will execute `su -`, and not your habitual shell.

By choosing a colored background, you create a root shell window that is clearly distinct from the others. Moreover, the title of this window will always contain the phrase **root shell**, even if the application changes it.

+   4. If you don't want to create a special launcher on your desktop or bottom panel, that's it: whenever you open a terminal window, you can choose **File | New Window** or **File | New Tab** and select the **root** profile instead of **Default**. Naturally, before having access to the root shell, you'll need to type the root password (no matter how acquainted you get with your Linux system, it will never trust you completely...)

+   5. If you want to create a **launcher** (that is, a personalized icon), then click with the right mouse button on the desktop background and choose **New Launcher** from the menu that pops up. The **Create Launcher** dialog will appear:
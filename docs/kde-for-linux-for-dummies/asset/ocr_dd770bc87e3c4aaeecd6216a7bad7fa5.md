# Part IV: Under The Hood

How do you get to root if you're logged in as a user? Sure, you can log out of your user account and come back in as root, but that means shutting down all your active programs. That can be a little tricky if you're chatting with Ksirc or listening to a CD.

The trick lies in KFM. Use the file manager's *superuser mode* to access root capabilities, get your task done, and then get back to whatever it was you were doing before:

+   1. Open the KDE menu and choose **System:: File Manager (Super User Mode)**.

A terminal window appears; it is not the regular KFM window. The terminal window contains a prompt for the *root* password, as shown in Figure 13-1.

![](bbox=[0.24, 0.405, 0.72, 0.66])

+   2. Enter the **root password** and press **Enter**.

KFM appears. Notice that it's showing the */root* directory, which it doesn't do when in regular mode.

+   3. Access the file or run the program for which you need root access.
+   4. Choose **File::Close** to exit KFM.

This is a useful way to check something quickly - a configuration file, for instance.

# The perils of multiple users

Let's face it. People can be weird. Sometimes they can even be offensive. More often, they can get themselves into trouble without even knowing it.
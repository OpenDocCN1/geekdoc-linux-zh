
## Configuring User Accounts

In Project 7A, you learned how to set up additional user accounts, a pretty easy endeavor, all things told. There are, however, a few settings you can apply to those user accounts that might be of interest to you. In order to access these features, you must first open the **User Accounts** module by clicking **System Administration** in the left pane of the Control Center window, and then clicking **User Manager**. When the User Manager module appears in the right pane of the window, click the **Administrator** button at the bottom of the window, and then supply your root password when prompted to do so. You will then be ready to perform either of the settings changes I will now describe.

### Limiting Login Availability

One of these settings that you might find handy is limiting the time and/or days that a user can log in to the system. For example, let’s say that you don’t want your kids playing around with the computer when you are at work or when they should be doing their homework . . . or playing outside to get some exercise.

To set things up in this way, just follow these steps:

- 1. Select the username of the user for whom you wish to limit access in the User Manager module (by clicking on that user’s name once), and then click **Properties**.

- 2. In the **User Properties** window that appears, click the **Account** tab.

- 3. Once in that tab, click the checkbox next to the words *Only allow user to login between*.

- 4. Now set the times and days that you want the user in question to have access to your computer. When done, your window should look something like that in Figure 7-19.

![](img/3badae5570de77b990135448f8a8a1cc_142_0.png)

- 5. Once you have finished, click **OK** to close that window, and then click **Apply** in the Control Center window.

### Locking an Account

You can also just lock an account, thus prohibiting a given user from accessing your computer until you wish to allow them to use it again. For example, you might want to make sure that your daughter finishes that essay that is due next week, and so until she does you don't want her to be playing around on the Internet. You can block her account from the same **Account** tab mentioned in the previous section. Click your username before opening the User Properties window, and then click the checkbox next to the words *Lock User Account*. Of course, when you are ready to provide access again, just uncheck the box, and all will be back to normal.

## Dual-Booters: Changing the Default Operating System on Boot-Up

If you have a Xandros/Windows dual-boot setup, you no doubt already know that when you start up your machine, you are given the choice of which operating system to boot up. The default system in such a setup is Xandros, which means that if you make no choice at the time, your machine will automatically boot up into Xandros, but you will have to use your cursor and ENTER keys to select Windows.

If you would prefer to have Windows as the default boot-up system, you can do so in the Control Center window by following these steps:

- 1. Click **System Administration** in the left pane of the Control Center window.

- 2. In the subcategories that appear below System Administration, select **Boot Manager**.

- 3. When the Boot Manager module appears in the right pane of the window, click the **Administrator** button at the bottom of the window, type your root password when prompted to do so, and then click **OK** in that password window.

- 4. Once in root mode, click the drop-down menu button next to the words *Default operating system* (the button itself will be showing the version of Xandros you are using, such as *Xandros Desktop 3.0.1 OC*), and then select the version of Windows you are using in the drop-down menu (Figure 7-20).

![](img/3badae5570de77b990135448f8a8a1cc_143_0.png)

*Figure 7-20: Changing the default operating system in dual-boot setups*

- 5. If you would also like to decrease the default auto boot-up time (the time before the system automatically boots up when you do nothing—the default is 30 seconds), adjust the numbers in the box to the right of the words *Automatically start default operating system after*.

- 6. Once you have finished making the changes, click the **Apply** button, and then quit the Control Center.

The next time you start up your machine, you will, as usual, see the boot-up screen; however, if you do not manually select Xandros at that time, your machine will automatically boot up into Windows.

# 8

# THE KEYS TO THE GATES OF OZ, OR THE GATES OF XANDROS ANYWAY

*Expanding and Updating Your System via Xandros Networks*

![](img/3badae5570de77b990135448f8a8a1cc_144_0.png)

I mentioned in Chapter 1 that the first time I ever heard of Xandros was from a friend who described the system as “cool.”

Well, when I first gave Xandros a try, I thought it was really good and, more importantly, incredibly easy to use—easier, in fact, than Windows. The word “cool,” however, didn’t immediately pop into my mind. That is, until I first used Xandros Networks.

What is Xandros Networks? Well, it is sort of a combination of things—a simple-to-use application (Figure 8-1) and a set of online repositories that houses an amazing array of applications and related files. The Xandros Networks (XN) application acts as an interface via which you can access those repositories and then easily download and install whatever you find of interest there. Now, I admit that what I’ve just described, on its own, might not initially sound all that impressive, but if you have a better understanding of what it is normally like to install an application in Linux, however, you will see why Xandros Networks is nothing short of a godsend.

![](img/3badae5570de77b990135448f8a8a1cc_145_0.png)

# Figure 8-1: The Xandros Networks application

When you install an application in Linux, that application usually requires that you also install one or more other files that it needs in order to function. These files are called *dependencies*, and some dependencies have dependencies of their own. And, need I say that some of those dependencies have dependencies of their own. Chasing down, installing, and getting all those different parts to work correctly on your own can be a time-consuming and sometimes frustrating experience. This recurring dependency chase is often referred to as *dependency hell*, and rightfully so.

This is where the “cool” comes into play. When you use Xandros Networks to download and install an application, XN also automatically downloads and installs all of the dependencies required in order for the application to run. So you don’t have to do any chasing down of this or that file, and you can be pretty sure that whatever you download will, in fact, run—and run as it is supposed to.

## Impressed yet?

If you still aren’t convinced, think about this: almost 98 percent of the applications available via Xandros Networks are free. Sure, you won’t get the pretty boxes and shiny shrink-wrap that you do when you buy a Windows application at the local computer store, but, hey . . . I said free! How can you not love that, eh?

And what about that other 2 percent that aren’t free, you ask? Well, most of those apps are commercial offerings that you would have to pay for anyway, but when they’re downloaded and installed via Xandros Networks, you can be sure that they will work on your system. These include applications such as CrossOver Office, which allows you to run certain Windows applications (such as MS Office) on your Xandros system, or popular games such as Quake III and Return to Castle Wolfenstein.

## Xandros Networks First Time Out

Well, let’s stop babbling about what Xandros Networks is and instead put it into action. To run XN, just double-click the Xandros Networks icon on the desktop, or go to the Launch menu and select Xandros Networks. (Xandros Networks is an Internet application, so you will have to be connected to the Internet when doing this.) After a few seconds, the Xandros Networks application will appear, and the first time out, it will go through a series of steps that are mostly hands-off for you.

The first thing Xandros has to do, and it will do this every time you start it up, is take inventory of what is already in your system, thus providing it with a database that it can check in the future when you download applications. This allows Xandros Networks to know just what it needs (and doesn’t need!) to download in order to make your application work. During this time, you will see a Progress Update window (Figure 8-2), which will automatically disappear when the process is finished.

![](img/3badae5570de77b990135448f8a8a1cc_146_0.png)

*Figure 8-2: Xandros Networks indicates its progress as it takes inventory of your system*

In the next phase, Xandros Networks has to check out its online repositories in order to see what is available for you there.

In the small window that appears (Figure 8-3) asking for your permission to do so, click OK, and the process will be strictly hands-off from there on in.

![](img/3badae5570de77b990135448f8a8a1cc_146_1.png)

*Figure 8-3: Xandros Networks asks your permission to do an online search of available packages*

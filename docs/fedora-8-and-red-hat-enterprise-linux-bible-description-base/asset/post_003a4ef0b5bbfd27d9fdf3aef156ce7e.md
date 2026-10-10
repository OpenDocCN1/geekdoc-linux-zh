
## Amazon
Create links to your Amazon profile, reviews, and wishlist.

## Del.icio.us
Save and organize a collection of favorite Web sites.

## Digg
Connect to your account on Digg.com to view and vote on popular stories.

## Facebook
Get to your Facebook social network site.

## Flickr
Visit your online digital image collection at Flickr.com.

## Lots of Others!
Besides those just mentioned, Mugshot lets you create connections to your accounts with Google, MySpace, Netflix, Picasa, Rhapsody, YouTube and others.

- **Add People** — From your Mugshot account, select Active People to get to a link where you can invite friends. Once you invite a friend and the friend accepts, the person is added to the People section of your sidebar.

- **Add Groups** — From your Mugshot account, select Active Groups to see available Mugshot groups. Select Join Group to add it to a list of groups that you follow.

When you’ve completed these configuration steps, your Online Desktop should be ready to use. Figure 3-17 shows an example of an Online Desktop and related Mugshot information.

![](img/fb202c163797a743c3c6cf236316bc96_150_0.png)

After logging in to Mugshot, you’ll see the following information, starting from the top of the Big Board sidebar in Figure 3-17:

- **User Information** — The user name and face image appears in the top box of the My Desktop sidebar. Select that box to logout of the desktop, visit the Mugshot account page, view system preferences, or minimize the sidebar.

- **Tiny Icons** — The tiny icons below the User Information represent the online services you have configured for your Mugshot account. Beginning with the top-left icon in this example, the icons represent Digg, Picasa, Amazon, Netflix, Del.icio.us, my home URL, Reddit, Twitter, and Flickr.

- **Search Box** — Type a term into the search box (flash memory appears in this example) and press Enter. A pop-up lets you select to search for that term at Amazon.com, Answers.com, Creative Commons, eBay, Google, or Yahoo.

- **Files** — See the files that you have opened recently under the Files box. Select More to search or browse for local files.

- **Applications** — Your most-used applications appear in the Applications box, ready for you to start at any time. Select More to search for an application or see statistics about the types of applications you use most.

- **People** — The people you added to your Mugshot account appear, with their names and icons, in the People box. Click on a photo or name to go to that person’s Mugshot page.

- **Calendar** — Connect to your online Google calendar from this box.

- **Mugshot Home** — In the example, a Web browser is open to my Mugshot home page. From the Mugshot home page, you can access the same services that are loaded on your Online Desktop, as well as configure all the features that are picked up by your Online Desktop.

- **Mugshot Stacker** — Click the Mugshot icon in the panel to see the Mugshot stacker. That stacker shows information about your activities, as well as activities of others you have added to your People list. In this example, you can see that I joined a group, left another group, and added a movie to my Netflix queue.

Because Online Desktop is still under development, expect to have many more features and services available by the time you read this text. In particular, work is being done to integrate online applications, so you will be able to work with Web applications to use your documents, spreadsheets, and other important information.

## Switching Desktop Environments

If you decide you want to try a different desktop environment, the Desktop Switcher provides a graphical means of changing your desktop environments between KDE, GNOME, and several different window managers (including TWM). To open the Desktop Switcher, select System ➔ Preferences ➔ Desktop Switching Tool.

From the Desktop Switcher, select the desktop environment (GNOME, KDE, or Xfce) or window manager (TWM) you want to use next. You can have that change apply to the current display (just the next time you restart X only) or make the change permanent. Click OK. Then log out. The next time you log in, the new environment or window manager will take effect.

> **NOTE:** To use the Desktop Switcher window, you must have the switchdesk-gui package installed. Otherwise, you can use the `switchdesk` command, followed by the name of the Desktop you want to switch to, from a Terminal window to change your Desktop.

If you just want to change your desktop environment temporarily, you can select Session from the login screen and choose the desktop you want. You can choose it just for the current session or to have it be your default desktop.

## Using the KDE Desktop

The KDE desktop was developed to provide an interface to Linux and other UNIX systems that could compete with Mac OS or Microsoft Windows operating systems for ease of use. Integrated within KDE are tools for managing files, windows, multiple desktops, and applications. If you can work a mouse, you can learn to navigate the KDE desktop. Fedora 8 includes version 3.5.8 of KDE.

> **NOTE:** KDE is not installed by default for Fedora. Therefore, to use the procedures in this section, you might have to install KDE. During installation, you could use a Custom install type to install KDE. Otherwise, see Chapter 5 for information on how to use the Package Management window or yum to add KDE. The Fedora 8 Desktop Live CD also does not include KDE; however, the Fedora project does produce a Fedora 8 KDE Desktop Live CD that you can download from a Fedora mirror site.

The lack of an integrated, standardized desktop environment in the past has held back Linux and other UNIX systems from acceptance on the desktop. While individual applications could run well, you rarely could drag and drop files or other items between applications. Likewise, you couldn't open a file and expect the machine to launch the correct application to deal with it or save your windows from one login session to the next. KDE provides a platform for developers to create programs that easily share information and detect how to deal with different data types.

The following section describes how to get started with KDE. This includes using the KDE Setup wizard, maneuvering around the desktop, managing files, windows, virtual desktops, and adding application launchers.

## Starting with KDE

You can select the KDE desktop from the login screen (provided that KDE is installed). Choose Session → KDE. Then type your login name and password, as prompted. The KDE desktop should appear, as shown in Figure 3-18.

![](img/fb202c163797a743c3c6cf236316bc96_153_0.png)

Figure 3-18: Manage files and applications graphically with the KDE desktop.

## KDE desktop described

You may notice that, in Fedora and RHEL, KDE looks very similar to GNOME. That’s because both begin with the same icons and background. Beneath the surface, however, you will notice that there are a lot more tools with KDE for configuring and using your desktop.

Here are some descriptions of what you will find on the KDE desktop for Fedora and RHEL:

- **Desktop icons** — The desktop starts out fairly sparse, with only a Trash icon on the desktop.

- **Panel** — The panel provides some quick tools for launching applications and managing the desktop. You can adapt the panel to your needs by resizing it, adding tools, and changing the look-and-feel. By default, you start with a home folder and Konqueror icon.

- **K menu** — This panel button is represented by a K logo. Click this button to see a menu of applications, utilities, and configuration tools that are available to run on your KDE desktop.

- **Desktop Pager** — This box on the panel consists of your virtual desktops, which contain small views of each desktop. There are four virtual desktops available to you, by default. These are labeled 1, 2, 3, and 4. You begin your KDE session on virtual desktop 1. If there are windows on the desktop, small icons representing them may cover the desktop number. You can change to any of the four desktops by clicking it.

- **Taskbar** — This button shows the tasks that are currently running on the desktop. The window that is currently active appears pressed in. Click a task to toggle between opening and minimizing the window.

- **Klipper** — This button looks like a clipboard. Click it if you want to clear your desktop’s clipboard.

- **Clock** — The current time and date are shown on the far right-hand side of the panel. Click them to see a calendar for the current month. Click the arrow keys on the calendar to move forward and back to other months.

- **Konqueror** — The default file manager for KDE.

- **KDE Control Center** — The window for configuring the desktop environment in KDE.

### Getting around the desktop

Navigating the desktop is done with your mouse and keyboard. You can use a two-button or three-button mouse. Using the keyboard to navigate requires some Alt and Ctrl key sequences.

### Using the mouse

The responses from the desktop to your mouse depend on which button you press and where the mouse pointer is located. Table 3-2 shows the results of clicking each mouse button with the mouse pointer placed in different locations.

The mouse actions in the table are all single-click actions. Use single-click with the left mouse button to open an icon on the desktop. On a window title bar, double-clicking results in a window-shade action, where the window scrolls up and down into the title bar.

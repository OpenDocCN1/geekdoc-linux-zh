
# Chapter 5: Using the GNOME Desktop

## Tip

In addition to the Tracker-related applications discussed in this section, the tracker-utils package provides some other useful utilities, such as the tracker-stats and tracker-status utilities that provide information about the searches that Tracker has performed, how Tracker is performing in general, and so on. ■

## Using the GNOME Deskbar Applet

Deskbar applet, how do I love thee? Let me count the ways. I love thee when I forget the name of the file in which I stored the great novel or my mother's recipe for milky beans, or when I need to look up a word in a dictionary or thesaurus, or when I want to search the Web. And of all, I love thee when I don't want to start specific applications for each of these different, but related, tasks.

The Deskbar applet is a one-stopping applet for any search task that I can think of, including searching for non-file-related data such as specific applications and windows. The Deskbar applet includes some useful hooks for performing common system tasks, such as logging out, suspending your system, and even shutting it down.

The Deskbar applet is not installed by default on an Ubuntu system, but can be easily installed by installing the deskbar-applet package using your favorite package management tool. If you want to use the Deskbar applet with Tracker (and who wouldn't?), you must also install the libdeskbar-tracker package.

Once installed and added to the GNOME panel, the Deskbar applet is accessed by clicking on its icon "magnifying glass and more" icon. Figure 5-35 shows the Deskbar applet dialog, which displays after clicking on this icon. (This looks slightly different on different Ubuntu releases, but the functionality is the same.)

### FIGURE 5-35
The initial Deskbar applet dialog

![](img/1a233c34336fbf5a85d6eb785e401709_218_0.png)

Figure 5-36 shows the default results of a search for the word Ubuntu on one of my systems. You can see from the position of the elevator button in the scrollbar at the right of this dialog, these results are only the tip of the iceberg—there are many more possible results.

Search results in the default configuration of the Deskbar applet are organized into various sections, including Actions (programs that you can execute whose name matches your search term), Documents that match your search term, Files with unrecognizable extensions, or MIME types whose path or filenames match your search terms, and so on.

# Part II: Ubuntu for Desktop Users

## FIGURE 5-36

A search for Ubuntu in the Deskbar applet

![](img/1a233c34336fbf5a85d6eb785e401709_219_0.png)

Simply pressing Return will execute the first item in the list, or you can click on a specific result to perform the associated action, whether it's opening a file or performing a Web search for your search terms. Empty sections are not displayed—for example, if no video file matches your search terms, there won't be a Videos section. However, as you can see, there's a whole lotta search going on, and all of it available through this single applet. Personally, that's too much data for me—I prefer to reduce the overwhelming number of possible locations that are offered in response to a Deskbar applet search by configuring it to search only some of my favorites. To configure the locations that the Deskbar applet will query (or offer as additional queries), right-click on its icon in the panel and select the Preferences menu option to display the "Deskbar Preferences" dialog shown in Figure 5-37.

### FIGURE 5-37
Configuring search locations for the Deskbar applet

![](img/1a233c34336fbf5a85d6eb785e401709_219_1.png)

# Chapter 5: Using the GNOME Desktop

The search tab in this dialog enables you to configure both locations that will be queried for your search terms and the order in which those locations will be queried. Search options that are enabled are preceded by a check mark, and they are searched in the order that they appear. To enable or disable a search option, click the checkbox. You can also change the order in which search options appear by selecting the name of a search option and dragging or dropping it to a new position in the list, or by using the Top/Up/Down/Bottom buttons to change its position.

Everyone's id of what and where to search are different, but I reconfigure the Deskbar app to use the following search options, in the following:

- Tracker Search: I'm often looking for data in a file that is somewhere on my system, so putting this option is a good complement to my web search options.
- Dictionary: Believe it or not, I am occasionally at a loss for words (or at least the right one), so it would be useful to look up words in an online dictionary.
- Google Search: Submit my search terms to the Google search engine. I put this third because it offers more possible actions than the first two.
- History: It makes easy to reuse searches, in case I want to pursue some subject in more detail, find a specific file, and so on

As you can see, the Deskbar app is a great complement to the Tracker family of desktop search applications. It is extremely convenient to be able to initiate a search for something from a single location, and it is sufficiently configurable to enable you to tailor your search preferences to the locations and types of searches that you typically want to perform.

## Using a Window Manager

The first section of this chapter, “What's a Desktop? Graphical Environments for Linux,” discussed the differences between window managers and desktops, and hinted at the fact that more X Window System window managers are available than you could shake a stick at. Popular window managers include AfterStep, Blackbox, Compiz, Enlightenment, Fluxbox, FVWM, IceWM, KWin, Metacity, vtm, VTWM, and Window Maker, but there are many, many, many.

After experiment with GNOME for a while, you might be curious about what these window managers look like and how they work. Half the fun of a flexible computing environment such as Linux and the X11 system is experimenting with new software “because it's there.” You might be interested in window managers if you are running Ubuntu on a slow system or a system with a limited amount of memory, such as many older laptops, because window managers require less memory and other system resources than complete desktop environments like GNOME.

As you might, it is extremely easy to temporarily switch between GNOME and a specific window manager. First, you have to install one or more window managers using any of the software update tools that are also discussed in Chapter 19. After installing window managers and logging out, you can start any installed window manager by selecting the name of the user that you want to log in to display the session options at the bottom of the login screen. Click the down-arrow to the right of the Sessions option to see the list of available session managers.

### FIGURE 5-38
The GNOME login screen's Sessions menu

![](img/1a233c34336fbf5a85d6eb785e401709_221_0.png)

Figure 5-38 shows a sample Sessions menu on an Ubuntu system where a few window managers (FVWM, IceWM, and Fluxbox) have been installed. Select the window manager that you want to start, enter your password in the login dialog, and press Return or click Log in. As an example, selecting “IceWM” would start the IceWM window manager, as shown in Figure 5-39.

### 5-39
The IceWM window manager on an Ubuntu system

![](img/1a233c34336fbf5a85d6eb785e401709_222_0.png)

You can permanently customize the window manager that is started when you log in by using the System $\leftarrow$ Administration $\leftarrow$ Login Screen menu command. After selecting this menu item, clicking Unlock to make changes, and entering your password, you can select the window manager that you want to start from the Select drop-down list at the bottom of the dialog shown in Figure 5-40.

You can also change the window manager that your Ubuntu system starts using a text editor to create a file called .xsession in your home directory, which contains a line like the following:

```
exec /usr/bin/icewm
```


## Klaptop

An application that appears if you’re using a laptop computer. It allows you to check the status of your batteries and adjust relevant settings. (Looks like an electrical plug next to a battery.)

## Sound Mixer

A control that allows you to adjust the overall volume of your system. (Looks like a small speaker.)

## Xandros Update

An application that periodically checks with Xandros Networks for the availability of system updates. (Looks like a small globe, most likely with an exclamation mark in a small square.)

## Lock / Logout

A pair of buttons with which you can log out (right button—looks like a power button) or lock your screen (left button—looks like a lock). Locking your screen is a handy means of keeping other people’s noses out of your business while you sneak away from your desk to get a cup of coffee. When you click the Lock Screen button, Xandros will run a screen saver (or just blacken your screen if no screen saver is selected). To use your system again, just move the mouse or press any key and Xandros will prompt you for your user password. Once you input the password, the screen saver will disappear, and you can get back to work or whatever else it was you were doing.

## Switch User (not shown)

This button, which shows two people standing, appears only on systems whose video card drivers support it. It allows you to switch between user sessions without having to quit running applications. A sort of logout without really logging out.

## Clock

The obligatory and ubiquitous desktop clock and calendar.

## Hide / Show Panel

Click this button to hide or show the Panel. (Looks like a small black arrow.)

## Project 3B: Customizing the Panel

The Panel is not a static thing. You can add launchers (program shortcuts or aliases), utilities, and even amusements to make it do almost anything you want it to, within limits, of course. In the various stages of this project, you will customize your Panel to make things more convenient for you as you make your way through the rest of this book. You are, of course, free to change any of the customizations I ask you to make, or to just pick those that are of interest to you, but I’d suggest performing at least a few of them so that you can get a feel for things.

Each of the following subprojects is very simple. Most are point-and-click procedures that you should be able to handle without any difficulty.

### 3B-1: Deleting a Launcher from the Panel

Deleting items from the Panel is a very simple procedure. A good candidate to work with is the Help Center launcher, because it also appears in the Launch menu and this is an extra copy. Freeing up Panel space will make room for other items more to your liking that you may want to add.

To delete the Help Center launcher, here is all you have to do:

- Right-click the **Help Center** launcher in the Panel.
- In the pop-up menu, select **Remove Help Button**.

### 3B-2: Adding a Launcher to the Panel

Now that you have an empty space left behind from where the Help button used to be, let's fill it in with something more useful. A good candidate would be the Calculator, which everyone needs to use at one time or another.

Here's how to add the launcher:

- Right-click the open space left behind after removing the Help button.
- From the pop-up menu, select **Add Application Button ► Applications ► Accessories ► Calculator**.

### 3B-3: Adding a Menu to the Panel

You can add whole menus to the Panel as well as application launchers. A good choice would be the OpenOffice.org menu, because most people use these applications quite frequently.

Here's what you do to add the menu:

- Right-click the open space to the right of the Calculator launcher you've just added.
- From the pop-up menu, select **Add Application Button ► Applications ► OpenOffice.org ► Add This Menu**. Be sure to select **This Menu** in the very last submenu that appears, as shown in Figure 3-7.

![](img/3badae5570de77b990135448f8a8a1cc_62_0.png)

### 3B-4: Moving Items Within the Panel

When the OpenOffice.org menu button that you added to the Panel in Subproject 3B-3 appears, it will most likely be located far from the other application launchers that are at the left side of the Panel. Having the menu over there with the others would be the most logical arrangement, so in this part of our project we are going to do some moving.

Here’s what you do to move the menu button:

- Right-click the OpenOffice.org menu button (or any other Panel item you want to move that won’t move by dragging alone).
- From the pop-up menu, select Move OpenOffice.org (or whatever the name of the item you’re trying to move is).
- Your cursor will now look like an arrowhead-tipped crosshair. Without holding down either mouse button, move the mouse to the location where you would like to place the menu button—in this case, just to the right of the Calculator launcher. The menu button will follow along.
- When the menu button is where you want it to be, click the left mouse button, and you’ll be done.

### 3B-5: Adding a Quick Browser for Your Home Folder to the Panel

In addition to application launchers and menus, you can also add Special Buttons to the Panel. The Launch and Show Desktop buttons are examples of these Special Buttons. A very handy Special Button you might want to consider adding is a Quick Browser. A Quick Browser allows you to view the contents of any folder you specify, in menu form, from the Panel. A logical and convenient choice for this project would be a Quick Browser for your Home folder, an example of which you can see in Figure 3-8.

Here’s what you need to do to add a Quick Browser for your Home folder:

- Right-click any open space in the Panel.
- In the pop-up menu, select Add ▶ Special Button ▶ Quick Browser.
- The Quick Browser Configuration window will now appear. The default path in the text box next to the word Path will be /home/your_username (mine, for example, says /home/rjg). Click OK.

### 3B-6: Adding a Weather Monitor to the Panel

In addition to application launchers and menus, you can also add mini-programs (called *applets*) to the Panel. Each of these applets performs a specific function, usually adding a bit of convenience to your desktop in the process. The applets at your immediate disposal include an in-panel sound-configuration tool, a dictionary lookup input box (discussed in Chapter 13), and the Clock, which is already present in the Panel by default. One the most popular applets, however, is the weather monitor, called KWeather.

![](img/3badae5570de77b990135448f8a8a1cc_64_0.png)

*Figure 3-8: A Quick Browser button for your Home folder in action*

You should note that because this applet periodically uses the Internet to check for the current conditions in the location you choose, it is best used if you have an uninterrupted Internet connection such as cable or DSL. Here's how to add the Weather applet:

- Right-click any empty space in the Panel.
- From the pop-up menu, select **Add ▶ Applet ▶ Weather**. A warning message will most likely appear at the top-left corner of your screen saying, “The requested station does not exist.” This is logical enough, because you have not yet selected a weather station to monitor.
- The applet is added to the Panel. To select a weather station, right-click the **Weather** applet and select **Configure KWeather**. The KWeather Configure window (Figure 3-9) then will appear.
- In the configure window, click the blue link that says **Lookup Your ICAO Code**. Your web browser will then open up to the National Weather Service website.
- Scroll down to the section that says Display All Stations In A State (or Display All Stations In A Country, if you live outside of the United States). Select your state or country, and then click the button that says **Display All Stations In**.
- The page that then appears will list all the weather stations in that state or country. Find the location you want to monitor and note its four-letter code. Detroit Wayne County Airport, for example, is KDTW.

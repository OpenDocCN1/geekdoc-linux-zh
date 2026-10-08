
# Part II: Ubuntu for Desktop Users

- **About GNOME**: Displays information about the specific version of GNOME that you are running, as well as general information about the many wizards who have contributed to the GNOME project in one way or another. You will probably need to provide GNOME version information if you post problem reports or questions, or if you contact any of the Ubuntu vendors in the Ubuntu Marketplace.

- **About Ubuntu**: Displays online documentation for the Ubuntu Project, which includes information about the specific version of Ubuntu Linux that you are using. As with GNOME version information, you will probably need to provide Ubuntu version information if you post problem reports or questions, or if you contact any of the Ubuntu vendors in the Ubuntu Marketplace.

# Context-Sensitive Menus

The menus discussed in the previous section always display when you left-click on a specific menu heading or submenu, regardless of what else is happening on your Ubuntu Linux system. Context-sensitive menus display when you right-click on something on your Ubuntu Linux screen, but their contents depend on what you've right-clicked. Because their contents differ from the context in which you've right-clicked, these right-click menus are referred to as context-sensitive menus. Figure 5-4 shows the context-sensitive menu that you see when you right-click on any part of the background for your Ubuntu desktop.

FIGURE 5-4
The GNOME desktop's context-sensitive menu

![](img/1a233c34336fbf5a85d6eb785e401709_179_0.png)

To show how application-specific these different context-sensitive menus can be, Figure 5-5 shows the context-sensitive menu that displays when you right-click within the main window for the Firefox Web browser.

The contents of context-sensitive menus are application-specific, which means that you can't directly customize them. However, these menus can be customized by installing additional applications or applets, or (in the case of extensible applications such as Firefox or Nautilus) by installing extensions or plug-ins that add new capabilities and therefore provide associated menu items.

140

# Chapter 5: Using the GNOME Desktop

# FIGURE 5-5

A context-sensitive menu in the Firefox Web browser

![](img/1a233c34336fbf5a85d6eb785e401709_180_0.png)

# Customizing GNOME Menu

Ubuntu Linux provides two ways to customize the contents of the basic GNOME menu. The Ubuntu Software Center item at the bottom of the Applications menu makes it easy for you to add new applications to any of the preexisting ones defined on the Applications menu by installing them and creating their entries as part of the installation process. Using the Ubuntu Software Center menu item is discussed in the section of Chapter 19, "Adding, Removing, and Updating Software," entitled "Installing Software with the Ubuntu Software Center." This item is extremely convenient if you want to add some popular application to the Applications menu, but isn't much use if you want to add your own menus or create custom submenus of Main Application for specific applications. To do this, you will need to use the Preferences submenu. Selecting this menu item starts the Alacarte Menu Editor, which makes it easy for you to add anything (including custom submenus) to your existing GNOME menu.

141

# Part II: Ubuntu for Desktop Users

For example, suppose you wanted to create your own submenu called Favorites and begin adding entries for your favorite applications to it. To do this (adding the Emacs text editor to this menu as an example), do the following:

1. Select System Preferences ⇔ Main Menu to start the Menu Editor. This Menu Editor dialog consists of two panes: a Menu Catalog pane at the left and a Menu Contents pane at the top right that shows the current contents of the currently selected menu. The Applications menu is expanded when this dialog opens, as shown in Figure 5-6.

# Tip

You'll notice the Menu Catalog pane lists many menus that are not currently displayed on your system. This is because they are not marked to be shown (via the Show column) in the Menu Contents pane on the right, as shown in Figure 5-6. ■

FIGURE 5-6
Editing menus on your Ubuntu system

![](img/1a233c34336fbf5a85d6eb785e401709_181_0.png)

2. Click the "New Menu" button. A dialog like the one shown in Figure 5-7 displays (with no entries in the text fields).

# Chapter 5: Using the GNOME Desktop

FIGURE 5-7
Adding a new menu

![](img/1a233c34336fbf5a85d6eb785e401709_182_0.png)

3. Enter the name of the new menu that you want to create (I'm using Favorites in this example), add an optional comment that will be used as the tool tip for this menu, and click OK. The new menu will be added to the Applications pane, and the Applications menu entry in the Menu Catalog pane will expand to show the current contents of that menu (which should be identical to the list in the Menu dialog at the top right). Select the name of your new menu in the Menu Catalog pane. The contents of the new menu (i.e., nothing) display in the Menu Contents pane at the top right, as shown in Figure 5-8.

FIGURE 5-8
Viewing the new menu

![](img/1a233c34336fbf5a85d6eb785e401709_182_1.png)

4. Click the New Item button. A dialog like the one shown in Figure 5-9 displays.

143

# Part II: Ubuntu for Desktop Users

FIGURE 5-9

Adding a new entry to a menu

![](img/1a233c34336fbf5a85d6eb785e401709_183_0.png)

5. Enter the information about your new entry (in this case, the Emacs text editor) and click OK. The dialog boxes, and the new entry on your Favorites menu displays, as shown in Figure 5-10.

# Tip

If you don't know exactly where the application that you want to add is located, you can click Browse to play a Browse dialog that lets you navigate to and select the application for which you want to create a new menu entry.

FIGURE 5-10

Your new menu entry in the Menu Editor

![](img/1a233c34336fbf5a85d6eb785e401709_183_1.png)

6. Select the Applications menu in the Menu Catalog pane at the left, and make sure that the checkbox in the Show column for your new menu is selected in the Menu Listing pane at the top right, as shown in Figure 5-11. This entry is required so that the menu is listed in the Applications menu once you exit from the Menu Editor.

# FIGURE 5-11

Making sure that the new menu is visible

![](img/1a233c34336fbf5a85d6eb785e401709_184_0.png)

7. Click Close to exit from the Menu Editor and add your changes to the Applications menu. The Applications menu is updated, and your new menu and entry are now available, as shown in Figure 5-12.

# FIGURE 5-12

Your new entries on the Applications menu

![](img/1a233c34336fbf5a85d6eb785e401709_184_1.png)

185

# Part II: Ubuntu for Desktop Users

If you decide not to save your changes, you can click the Revert button to undo your changes, and then click Close.

The flexibility in the dialog shown in 5-9 makes it easy to create menu entries for applications you have manually compiled and installed, such as in corporate or academic environments.

# Tip

You can also add menus in GNOME using the Nautilus File Manager, but I find that using applications designed editing menus is easier to understand. For information about Nautilus to create menus and menu items, see the online GNOME Users Guide

# Customizing Your Desktop

As explained earlier in this chapter, GNOME makes it easy to customize your menus and the applications they contain. Luckily, every part of the GNOME desktop is similarly configurable. This section highlights how to do some of the most common customizations people do to make their systems easier to use and generally personalize them. Many other customizations are available, but discussing all of them could make this impossible to list. Let's focus on the highlights!

# Customizing Mouse Behavior

One of the most common customizations people want to do is to change how responsive the mouse is, in one way or another. Available customizations include:

- The mouse is configured for left-handed or right-handed users. The latter is the default, but may not suit you if you use your left hand to control the mouse.
- The speed at which the cursor moves and the amount of screen estate the mouse covers in relation to moving your mouse
- The period of time that can elapse between two clicks to consider them as a double-click (which opens the target) rather than simply two clicks (which simply selects something). If you have difficulty double-clicking, you can increase the double-click period.

All of these customizations are controlled by the System Preferences menu's Mouse application, which is shown in Figure 5-13.

This application provides two tabs that enable you to configure different aspects of the mouse: the General tab, where you can configure the behavior of the buttons and the speed and sensitivity of mouse motion, and the Accessibility tab, where you can configure the speed to perform actions to simplify the use of a mouse by people who may have difficulty using a mouse in a traditional fashion. The General tab is shown in Figure 5-13. To switch between different tabs, simply select the appropriate tab in the Mouse Preferences application.

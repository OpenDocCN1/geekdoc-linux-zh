
## This Panel Properties

Each Panel’s properties can be configured individually. To change the configuration of the active Panel, right-click the Panel and select This Panel Properties from the pop-up menu. You may also press the Main Menu button and select the Panel > This Panel Properties. This will bring up the Panel Properties dialog box as shown in Figure 15.23. In this box you can change the properties for the active Panel.

![](img/a3584dae761d2e3abed8bf40d7637389_622_0.png)

**FIGURE 15.23**: This Panel Properties dialog box

The Panel Properties dialog box contains two tabs to help you set the active Panel properties: Edge Panel and Background. An explanation for both of these tabs follows.

### Edge Panel Tab

**Position** This changes the position of the Panel on the screen. You may select either Top, Right, Left, or Bottom. The Panel will change position once you have pressed the Apply button.

**Minimize Options** The options here will enable you to either explicitly hide the Panel yourself using the hide buttons or auto hide when the mouse is not over the Panel. If you choose Auto Hide, you might want to disable the hide buttons here as well. You may also disable the hide button arrows graphics on the Panel as well.

### Background Tab

**Background** These options allow you to change the background of the Panel itself. You may choose, if you wish, to have the standard, Pixmap, or Color background. The standard look for the Panel is determined by the GTK theme you are running at the time. The Pixmap option allows you to choose an image to tile or scale to the Panel. The Color option allows you to specify a particular color for the Panel.

![](img/a3584dae761d2e3abed8bf40d7637389_623_0.png)

> **NOTE**
> An easier way to change the background of your panel is to drag-and-drop an image file from the GNOME File Manager onto the Panel. This will automatically change the background of the Panel to that image.

**Image File** If you choose to have a Pixmap for the background of your Panel, this will allow you to choose which image to use. If you press the Browse button, you can search for the file you want to use.

**Scale Image to Fit Panel** This allows a background image to scale to the size of the Panel. If not selected, images will tile to the panel.

**Background Color** If you choose to have your Panel one color, this button will launch a dialog box that allows you to specify which color to use.

## EDITING THE MAIN MENU

The Main menu is a repository for your applications and can be found on the Panel. The Main menu is preloaded with GNOME, but it can be configured to fit your work habits. The Main menu is broken up into two main subdirectories: System menus and User menus. The Menu Editor is available for you to add new applications to the Main menu but you can not add applications to the System menus if you are not the system administrator (root). In this section you will learn how to configure the Main menu with applications you wish to use everyday.

### Configuring the Main Menu

If you want to change properties of the Main menu or any other menu you have on your Panel, right-click the menu button and select Properties. This will launch the Menu Properties dialog box as shown in Figure 15.24.

![](img/a3584dae761d2e3abed8bf40d7637389_624_0.png)

The first selection item in the Menu properties dialog box is Menu Type. This will allow you to change the menu from a Main menu to a Normal Menu.

The other choices in the Menu Properties dialog box are submenu selections for Main menus. These selections allow you to choose what is in your Main menu in a submenu, or off:

- **System Menus** These menu items are the default applications that come with GNOME.
- **User Menu** This contains any menu item you added using the Menu Editor for your user account.
- **Another Level Menu** If you are using the Red Hat Linux build, this is the default set of applications that ship with it.
- **KDE Menu** If you are a user of the Kool Desktop Environment, you may choose to include the applications included in the KDE menus.
- **Debian Menu** If you are using the Debian Linux build, this is the set of applications that ship with it by default.

### Using the Menu Editor

The Menu Editor is a configuration tool for the Main menu. It is very useful in setting up your system to your requirements. The Menu Editor is started by clicking the Main Menu Launcher and selecting Settings > Menu Editor from the Main menu. This will launch the Menu Editor as shown in Figure 15.25.

![](img/a3584dae761d2e3abed8bf40d7637389_625_0.png)

The Menu Editor is divided into two main panels. The left side contains the menu in its default state. The right side contains a tabbed dialog box that allows you to add new applications to the menu.

On the left side in the menu tree, notice that there are two main menu lists, one for User menus and one for System menus. The User menus are for the current user and the System menus are for all users on the system. The prepackaged applications are all located in the System menus. Within the menu list on the left side you may open and close folders and see what is in your current menu by clicking the small plus signs beside the menus.

#### Adding a New Menu Item

If you want to add a new menu item, press the New Item button on the toolbar. A new menu item will be placed where the highlighted menu is. If you do not have a menu highlighted, it will be placed at the top of the menu tree. Select the new item and type in the information for the item in the dialog box on the right. Once the information is complete, press the Save button and the new menu item will be inserted where your cursor is on the menu tree on the right. You may then move the menu item by pressing the up or down buttons on the toolbar. You may also move the menu item by dragging it with your left mouse button.

![](img/a3584dae761d2e3abed8bf40d7637389_626_0.png)

> **NOTE** Keep in mind that you can not change the System menus unless you are logged in as root. If not, you can only add to and edit the User menus.

#### Drag-and-Drop in the Main Menu

The Menu Editor supports drag-and-drop functionality which will make your work easier. You may drag applications to the folders you wish them to reside in or re-arrange you folders completely.

If you would like to place a menu item onto the Panel, you can drag-and-drop the item from the menu to the Panel, and it will place a launcher there with all the appropriate properties set for you. If you prefer not to use drag-and-drop, you may also right-click the menu item and choose Add This Launcher to Panel from the pop-up menu.

## THE GNOME CONTROL CENTER

The GNOME Control Center (see Figure 15.2.6) allows you to configure various parts of your system using a collection of tools called *capplets*.

### Chapter Fifteen

These applets may be associated with the core set of GNOME applications or other applications for which the developers have written applets.

Your Control Center may contain more applets than are documented here, depending on the applications installed on your system.

The Control Center is divided into two main sections: the menu of configurable applets and the main work space.

Working with the Control Center simply requires you to select a applet from the menu on the left and double-click it. Once this is done, the work space will change, allowing you to configure the item.

![](img/a3584dae761d2e3abed8bf40d7637389_627_0.png)

**FIGURE 15.26**: THE GNOME Control Center

You may start the Control Center in one of two ways. To launch the Control Center without any particular active applet, select the Control Center menu item from the System menu. If you know which applet you would like to edit, start that applet by selecting the correct menu item in the Control Center menu.

### Desktop Applets

#### The Background Properties Applet

The properties for your background image can be set in the Background Properties applet (see Figure 15.27) by either selecting a color or an image. If you select a color, you have the option of having solid or gradient colors. If you choose to have gradient colors, you may choose between

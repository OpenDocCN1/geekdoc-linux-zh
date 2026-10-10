
## Anatomy of a KDE Window

The key elements of a graphical user interface — program windows with titlebars, and so on — are pretty standard and familiar to most computer users. A KDE window, such as the one shown in Figure 3-1, may look a little different from its counterpart in Windows or Mac OS, but most of the parts are easily recognizable.

![](img/8dd43d91b80664e771e0c0a824d7392d_72_0.png)

Figure 3-1: Taking inventory of window parts.

Here's a quick rundown on the main parts of a KDE window:

- **Titlebar:** The colored bar that runs across the top of the window normally displays the name of the program and/or the filename of the document that appears in the window. The titlebar also serves as a “handle” that you can drag with the mouse pointer to move the window.
- **Border:** Defines the edge of the window. The border also serves as a sizing handle that you can drag with the mouse pointer to expand or contract the size of the window on a given side.
- **Close button:** Click this button to close the window and exit the application or document that is running within the window.
- **Maximize button:** Click this button to automatically expand the size of the window to fill all the available space on your desktop. If the window is already maximized, the complementary Restore button replaces this button (usually labeled with two stacked rectangles). Clicking the Restore button returns the window to its previous unmaximized size and position.
- **Minimize button:** Also known as the Iconify button. Click this button to remove the window from your desktop without exiting the program within the window. After you click the Minimize button, the program continues to run, but is represented only by a button on the KDE taskbar and a listing in the Window List, not by an open window on any desktop.
- **Sticky button:** Click this button to toggle Sticky mode on or off. If you make a window sticky, it appears in the same place on all of your virtual desktops instead of being available on only one virtual desktop.
- **Menu button:** Click this button to open a menu of window management commands. The default Menu button (labeled with a plain horizontal line) is normally replaced by an icon for the program running within the window. But regardless of the appearance of the Menu button, clicking it has the same effect.
- **Sizing handle:** Click and drag the sizing handle at the lower-right corner of the window to resize the window along both the horizontal and vertical axis at the same time.
- **Window background:** The interior of the window is the domain of the program running within the window. The application controls everything that appears within the window including the menus, toolbar buttons, status bar, and the contents of the main work area. KWM doesn't do anything except set the default colors for the window background, text, menu text, and selected items.

KDE is a highly customizable environment, and that customization extends to the appearance of the buttons and other components of the KDE windows. Figure 3-1 shows a KDE window using the default KWM settings. Your windows may look very different — especially if you use themes to modify the appearance of your KDE desktop. The window borders may be rendered to look like thick metal pipes and the titlebar buttons may carry different symbols. However, despite cosmetic differences, the KDE window components still work the same.

## The KDE Custom Window Shop

You may be quite content to stick with the default settings of KDE for controlling the appearance and behavior of KDE windows and desktop. For the most part, the KDE developers have done an excellent job of selecting sensible defaults that create a highly usable windowing system. However, if you're the type who just loves to tinker with your system, KDE gives you ample opportunity to do so. You can manipulate an amazing array of settings to control almost every imaginable detail of window management. Although a few aspects of window design (such as specifying the image files used to render window borders and buttons) require hand-editing arcane configuration files (and are those beyond the scope of this book), most of the custom window settings are readily available in a series of convenient dialog boxes.

You can find most of the custom window controls on various tabs of the KDE Control Center in dialog box. To open the KDE Control Center dialog box, use one of the following techniques:

- Click the KDE Menu button and then choose KDE Control Center.
- Click the KDE Control Center button on the panel.

After the KDE Control Center dialog box appears, you can use the index tree on the left side of the dialog box to select the tab you want to work on. The following sections of this chapter detail the settings you can adjust on each of the tabs.

## Configuring the titlebar

Perhaps the most prominent feature of any window is its titlebar. You can adjust several aspects of the titlebar appearance by following these steps:

1. Open the KDE Control Center dialog box. Click the KDE Control Center button on the panel or choose KDE Menu->KDE Control Center. The KDE Control Center dialog box appears.
2. Choose Windows::Titlebar. The Titlebar tab appears, as shown in Figure 3-2.

![](img/8dd43d91b80664e771e0c0a824d7392d_74_0.png)

3. Adjust the settings on the Titlebar tab as needed.

You can adjust the following settings:

- **Title Alignment**: The three radio buttons in this area enable you to select the alignment of the title within the titlebar. You can select Left (the default), Middle, or Right.
- **Appearance**: The options in this area define the kind of background that appears in the titlebar. Select Shaded Vertically to specify a color blend from top to bottom in the titlebar. Select Shaded Horizontally (the default) to make the color blend go left to right. Select Plain to specify a solid color titlebar and select Pixmap to display an image as the background of the titlebar.
- **Pixmap**: If you select the Pixmap option in the Appearance area, the options in the Pixmap area become available. Click the Active Pixmap and Inactive Pixmap buttons to open dialog boxes where you can select image files to use for the background of the active and inactive window titlebars. Select the No Pixmap Under Text option to suppress display of the image as the background for the title text.
- **Mouse Action**: Select an action from the Left Button Double-Click Does drop-down list box to define what happens if you double-click the titlebar. The default, (Un)Shade, causes the window to collapse so that only the titlebar remains visible, thus occupying less space on the desktop. Double-click the collapsed window titlebar to reverse the effect and restore the window to its normal size.
- **Title Animation**: If a window title is too long to fit in the titlebar, KWM automatically scrolls the title back and forth in the titlebar. You can control the speed of the scrolling action by dragging the Title Animation slider left or right.

4. Click the Apply button.

KDE applies the settings to your desktop and windows.

## Configuring the buttons

The titlebar buttons are an important feature of KDE windows. They provide quick access to the most-used window controls. You can rearrange the buttons to place the buttons in the positions that are most convenient for you. Here's how:

1. Open the KDE Control Center dialog box.

Click the KDE Control Center button on the panel or choose KDE Menu->KDE Control Center. The KDE Control Center dialog box appears.

2. Select Windows→Buttons.

The **Buttons** tab appears, as shown in Figure 3-3.

![](img/8dd43d91b80664e771e0c0a824d7392d_76_0.png)

Figure 3-3: Controlling which titlebar buttons go where.

3. Select the position for each of the **titlebar** buttons.

You can set the position for each of the five titlebar buttons (**Minimize**, **Maximize**, **Sticky**, **Close**, **Menu**) by selecting one of three radio buttons (**Left**, **Right**, **Off**). The sample titlebar near the top of the **Buttons** tab previews your selections.

You can’t put more than three buttons at either end of the titlebar. If you attempt to place a fourth button on one end, KWM automatically turns off one of the other buttons at that end. You need to reselect another location for the disabled button.

4. Click the **Apply** button.

KDE applies the settings to your desktop and windows.

## Configuring mouse button actions

KWM provides a multitude of options for controlling what happens when you click a window with the mouse pointer. Depending on which mouse button you click, where you click the window, and whether the window is active or inactive, the mouse click can raise a window to the foreground or lower it to the background, move or resize the window, or pass the click to the application within the window. And all these details are configurable. Follow these steps to change the mouse settings:

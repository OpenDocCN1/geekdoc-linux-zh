![](bbox=[0.75, 0.0, 0.95, 0.18])

# Menus and Toolbars

# In This Chapter

+   - Using the GNOME mechanism to quickly construct menus and toolbars
+   - Using the recommended standard menu layout to help standardize GNOME applications
+   - Using push buttons, toggle buttons, radio buttons, sub-menus and -toolbars, icons, text, and popup dialog boxes

A menu is a hierarchical grouping of buttons that can be used to issue commands to the program. So is a toolbar (well, almost). One difference between the two is that a menu uses text as a button label and a toolbar uses a graphic for the label. Also, a menu keeps some of its parts hidden, while a toolbar generally keeps everything visible. They both can be oriented horizontally or vertically. Because toolbars and menus are basically the same, GNOME has chosen to use the same technique for defining both of them. There are some differences here and there, but in many cases, if you code the definition used to create a menu, you also can use it to create a toolbar.

This area of programming traditionally has been one of the less elegant areas in the development of X applications. While the menu system has worked quite well from the early days of X, there is no way it could be called intuitive on the part of the programmer. GNOME simplifies this process by providing the programmer with a way to define everything in arrays that are organized in the same way as the menu produced on the display.

# The Mechanics of a Menu Creation

A menu is made up of a row or column of buttons. We are accustomed to seeing a menu bar appear as a horizontal row of buttons across the top of a window. Selecting one of these buttons causes a vertical column of buttons to appear. Each button in a menu either causes another column of menu buttons to pop up or invokes a callback function inside the program. There are a few other things that can be done with menu buttons (such as creating toggle buttons and a group of radio buttons), but the two basic actions of using a button for selection provides the basis of all menu operations.
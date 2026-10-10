```
107 GNOMEUIINFO_SUBTREE(" Settings",settingsMenu),
108 GNOMEUIINFO_SUBTREE(" Windows",windowsMenu),
109 GNOMEUIINFO_SUBTREE(" Help",helpMenu),
110 GNOMEUIINFO_END
111 };
112 
113 GtkWidget *createMenus(GtkWidget *app) {
114 
115 GtkWidget *statusbar;
116 
117 gnome_app_create_menus(GNOME_APP(app),mainMenu);
118 
119 statusbar = gtk_statusbar_new();
120 gnome_app_install_statusbar_menu_hints(
121 GTK_STATUSBAR(statusbar),mainMenu);
122 gnome_app_set_statusbar(GNOME_APP(app),statusbar);
123 
124 return(statusbar);
125 }
```

Line 4 contains the dummy data that is to be passed to all the callback functions. Instead of this format, you can change the program to simply pass a NULL pointer.

To avoid the necessity of writing prototypes for the callback functions, they are placed at the top of the file. The function helpAbort() that begins on line 6 creates a standard GNOME About box. The other callback function, starting on line 24, is named dummyCallback() and is used as a placeholder for all of the menu items that require callbacks — it pops up the announcement that the chosen menu item has not been implemented.

The submenu defined on lines 29 through 36 is a dummy to be used in places where a submenu is needed. There is no standard definition of what it should contain.

The entire menu is defined on lines 38 through 111. Lines 101 through 111 determine the order of appearance of the top-level menu items. The File and Edit menus should be familiar. The View menu is application-specific and should be used to switch among different ways to view data (such as zooming, changing colors, or modifying the sort order). The Game menu is present only for game software. The menu labeled `custom` marks the spot where applications should add its own menu (or menus). The Settings menu is used to configure the application — it may have some toggle buttons on it, but it should have a Preferences selection, and the Windows menu controls which window is being displayed currently.

The entries in the menu are defined by macros that were designed especially for the purpose. For example, the macro GNOMEUIINFO_MENU_COPY_ITEM() on line 61 was designed to create a menu selection with the word Copy and use the standard copy icon. Three of these menus are shown in Figures 8-3 through 8-5.
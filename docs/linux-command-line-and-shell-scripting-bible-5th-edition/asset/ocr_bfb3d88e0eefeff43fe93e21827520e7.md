The script using the **kdialog** command isn’t very different from the one using the **dialog** command. The resulting main menu is shown in Figure 18.10.

![](bbox=[0.17, 0.19, 0.87, 0.4])

Now your simple shell script looks just like a real KDE application! There’s no limit to what you can do with your interactive scripts now.

# ## The GNOME environment

The GNOME graphical environment supports two popular packages that can generate standard windows:

+   - gdialog
+   - zenity

By far, zenity is the most commonly available package found in most GNOME desktop Linux distributions (it’s installed by default in both Ubuntu and CentOS). This section describes the features of zenity and demonstrates how to use it in your shell scripts.

# ### zenity widgets

As you would expect, zenity allows you to create different window widgets by using command-line options. Table 18.4 shows the various widgets that zenity can produce.

**TABLE 18.4** The zenity Window Widgets

| Option         | Description                       |
| -------------- | --------------------------------- |
| --calendar     | Displays a full month calendar    |
| --entry        | Displays a text entry dialog window |
| --error        | Displays an error message dialog window |
| --file-selection | Displays a full pathname and filename dialog window |
| --info         | Displays an informational dialog window |
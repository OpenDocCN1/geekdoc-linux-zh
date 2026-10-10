# FIGURE 18.8

The `meminfo` command output displayed using the `textbox dialog` option.

![](bbox=[0.34, 0.19, 0.73, 0.42])

# Getting Graphic

If you’re looking for even more graphics for your interactive scripts, you can go one step further. Both the KDE and GNOME desktop environments (see Chapter 1, “Starting with Linux Shells”) have expanded on the `dialog` command idea and include commands that produce X Windows graphical widgets for their respective environments.

This section describes the **kdialog** and **zenity** packages, which provide graphical window widgets for the KDE and GNOME desktops, respectively.

# The KDE environment

The KDE graphical environment includes the **kdialog** package by default. The **kdialog** package uses the `kdialog` command to generate standard windows, similar to the `dialog`-style widgets, within your KDE desktop. However, instead of having the clunky feel to them, these windows blend right in with the rest of your KDE application windows. This allows you to produce Windows-quality user interfaces directly from your shell scripts.

> **NOTE**
> Just because your Linux distribution uses the KDE desktop doesn’t necessarily mean it has the kdialog package installed by default. You may need to manually install it from the distribution repository.
# **LXQt** 8/10

This desktop environment is a combination of the GTK-based lightweight desktop LXDE and Razor-Qt, which was an equally lightweight, but far less mature, desktop that used the Qt toolkit.

Thanks to this combination, LXQt manages to pull off the look and feel of a modern desktop without being a drain on resources. You can find LXQt in the repositories of virtually all distributions, and if your favourite distribution has a version for under-powered machines, chances are it's running LXQt.

It adheres to the old but familiar desktop metaphor, with a status bar laden with icons at the bottom of the screen. The applications menu features the traditional categorised list of apps as well as a search box to help launch apps. LXQt offers a decent number of tweakable options that help customise the most commonly used aspects of the desktop.

![](bbox=[0.08, 0.49, 0.34, 0.6])

# **Moksha Desktop** 7/10

This is a fork of the Enlightenment E17 desktop and features Bodhi Linux-specific changes, which the developers have been patching into E17's code over the years.

Moksha is fairly intuitive and easy to customise. It employs tons of visually appealing gadgets to display system information. These gadgets can be placed on the desktop as well as the taskbar, or 'Shelf' in Moksha speak. The desktop can be completely controlled via keyboard and you can define your own keybindings. You can also use the settings panel to influence the look and feel of your installation.

However, unlike E17, Moksha isn't readily available in the repositories of many distributions. Another issue with the desktop is its applications menu. While it does give you access to other areas of the installation besides applications, it doesn't feature a search box which can be used to quickly launch applications.

![](bbox=[0.37, 0.49, 0.63, 0.6])

# **Openbox** 7/10

Openbox is readily available in the software repositories of most distributions. Its minimalist yet customisable nature make it a robust choice for experienced users.

Its window manager is in fact so barebones that you wouldn't even notice it's there. All you get, by default, is a wallpaper-less background and a cursor. An application menu only appears in the right-click context menu. You can use the menu to launch apps, which run within windows with the usual controls and behave as you'd expect in any desktop.

The window manager is often combined with various other lightweight elements on the desktop. For instance you can use either *Tint2*, *Plank* or *Docky* to create a taskbar, and *PCManFM* as the file and desktop manager. You can also customise different aspects of the window manager using the *obconf* tool. Extensive manual configuration may not appeal to all users.

![](bbox=[0.67, 0.49, 0.93, 0.6])

# # Performance

## Do they actually perform better than the fully fledged defaults?

It's very difficult to measure performance in terms of absolute numbers due to a lot of factors. Since we can't separate the desktop environment from the apps, we can't really measure their exact draw on resources. This means the consumption will vary from machine to machine and may go up or down depending on the number of installed apps.

Also, there is no one single point of measurement. For instance, an environment could be blazingly fast to load, but its resource consumption could be really high while it's supposedly idle because of the fact that it's prefetching or loading components in the background.

On our test machine, EDE idles at about 150MB. The figures go up when an app is launched, but quickly drop back when you close the app. On a related note, it's fairly quick at launching apps, with *LibreOffice* timed at 4.3 seconds.

Then there's Lumina, which isn't designed for Linux -- and that's probably why its startup takes about three times longer than EDE. It idles at around 210MB, but app launch times are only slightly slower with EDE. Its memory consumption also mirrors EDE, with highs recorded at the initial launch of apps.

Moksha is just as lightweight as EDE but its startup times and app launches are noticeably faster. While LXQt does take slightly longer to bring up the desktop, its app launch times are on par with Moksha.

Openbox is blazingly faster than the others. The startup time for the window manager depends on the number of elements it has to load. Once it's loaded, app launches are among the fastest of the lot.

# ### VERDICT

| | 8/10 | 9/10 |
|---|---|---|
| EQUINOX DESKTOP | 8/10 | MOKSHA DESKTOP | 9/10 |
| LUMINA | 8/10 | OPENBOX | 9/10 |
| LXQT | 8/10 | | |

There's a reason why the desktops featured in this Roundup are considered *lightweight*, and it's not because of the disk space they require.
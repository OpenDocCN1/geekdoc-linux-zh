# # Remove unwanted desktops

You can install as many desktop environments as you like - aside from taking up space on your hard drive, they don't consume any resources unless you're actually running one.

But there may come a time when you've finished experimenting with desktops, settled on your favourite (or favourites) and want to remove the rest. It goes without saying you shouldn't be logged into the DE that you're planning to remove.

With that prerequisite out of the way, removing the desktop is best done from the Terminal, particularly if you plan to remove all the software the DE installed alongside itself.

Here's the two commands you'll need:

```
$ sudo apt-get remove packagename
$ sudo apt-get autoremove
```

Replace *packagename* with the desktop's package name. *cinnamon, plasma-desktop* (KDE Plasma 5), *gnome*, *lxde* or *xfce4* (Xfce).

need in a package you're happy to look at. Despite their differences, you'll notice similarities between many Linux DEs. That's because they are basically variants of Gnome. Unity is the obvious example here, sharing many of its elements, but even the likes of Cinnamon betray their roots through the use of similar applications, built using the GTK toolkit that Gnome employs. The big rival to Gnome is KDE, and its differences extend beyond the fact it employs the Qt toolkit rather than GTK. For starters, it's one of the most configurable tools out there, which makes it more popular with advanced users.

There's also a question of performance and power consumption. Some desktops are more resource hungry than others, eg Unity and KDE Plasma 5. The increased demands do come with benefits, such as: a wider feature set, a bigger range of tools and flashier looks, which are missing from lightweight alternatives such as LXDE. But that means they're less suitable for older and low-powered machines.

The best thing to do is run a couple of them and see how they perform - you should notice those with a smaller footprint are the most responsive, particularly on slow PCs. They also place fewer demands on power consumption, which should benefit those running on batteries. Remember, thanks to the fact you can easily switch between desktops, you can mix and match - a low-powered desktop while on the road, with a more fully featured environment for when plugged into the mains.

You're ready to start experimenting with desktops, so how do you install them? In some cases you can simply search for the desktop using your distro's software centre, but for others you may have to manually add the repositories (repos) yourself before installing through Terminal.

In the case of Ubuntu, you'll find Xfce (type *xfce4* into the Search box to locate it). Gnome and LXDE are all available through the Software Center. Click 'More Info' when you've found one - because they usually ship with optional components added in, you might want to review these before clicking the 'Install' button. Cinnamon and KDE Plasma 5 require a trip to the Terminal. In the case of Cinnamon, enter:

```
$ sudo add-apt-repository ppa:ppa:ppa
$ sudo apt-get update && sudo apt-get install cinnamon
```

For KDE Plasma 5, use these commands:

```
$ sudo add-apt-repository ppa:kubuntu-ppa/backports
$ sudo apt-get update && sudo apt-get install plasma-desktop
```

# ## Working with desktops

Once you've installed a new desktop, log out of your account. When you find yourself back at the login screen you should see an icon next to your username. Click this and you'll see a list of available desktops appear - in some cases you'll see multiple options based on a single desktop. Select one, then enter your password and log in as normal to start using it.

When you log into a new desktop for the first time, none of your existing preferences will come across from your old DE (but don't worry, they're all still there, ready and waiting for you the next time you log back into your original desktop). One of the benefits of having to make changes to your new desktop early on is that it forces you to explore, giving you insight into how it works and what tweaks you can perform.

# # Customise your new desktop

![](bbox=[0.1, 0.96, 0.33, 0.0010500000000000002])

# 1. Tweak the taskbar

The Cinnamon's taskbar is called the panel and it split into three sections: menu button, app shortcuts and applets. You can pin app shortcuts to it by clicking 'Menu', right-clicking the app shortcut and choosing 'Pin to panel'. Right-clicking the panel reveals more options, like adding new applets or adding a second panel (choose 'Modify panel...').

![](bbox=[0.33, 0.96, 0.66, 0.0010500000000000002])

# 2. Customise look and feel

Click the 'Menu' button and select the 'System Settings' button to change the way Cinnamon looks. In the Appearance section, you can change the background and system font (you'll see options from other desktops you've installed too). Selecting Themes and clicking 'Add/remove desktop themes...' you can download more themes to pick from.

![](bbox=[0.66, 0.96, 0.9, 0.0010500000000000002])

# 3. Change behaviour

Hot Corners enable you to specify actions that occur when your mouse goes into a corner of the screen, such as showing the desktop or displaying all workspaces. Windows is where you can edit the way windows behave and alter the display of the task switcher. Finally, the Extensions allows you to customise using third-party plugins.
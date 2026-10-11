
# Tutorial: Plasma 5

## Use Plasma 5 in VirtualBox

Hardware-accelerated desktop is a killer feature of Plasma 5, yet the downside is its unenviable performance as a guest in VirtualBox. The fix may sound brutal, but turning off 3D acceleration in the machine settings does the trick. You may also encounter the incorrect scaling of fonts and icons - this time you'll have to manually set the font DPI size in the KDE font settings.

## Make use of the Windows key

Many new Linux users come from the world of Windows where there are a number of keyboard shortcuts and other features that people get familiar with. Those who use GNOME on a Linux PC or OS X on a Mac know that the desktop metaphors are completely different and a user is supposed to change their habits in order to work efficiently on a new desktop. In KDE things are quite reversed: you can reproduce certain keybindings to work just the same as they do in Windows. In this example we will use the Windows button to launch the Start menu.

The default KDE Plasma desktop doesn't let you assign actions on a single key, but there's a workaround called KSuperkey. Once it is installed, just launch it with the `ksuperkey` command (and add it to KDE's autostart section) and then just hit the Windows key - in KDE it is detected as Meta. KSuperkey works fine with the default Plasma 5 Application launcher.

For the first trick we'll need the `wmctrl` package, which can be found in almost any Linux distro. Once you have it, create a script with the following content:

```sh
#!/bin/sh
target=on
if xprop -root _NET_SHOWING_DESKTOP | fgrep "= 1"; then
    target=off
fi
wmctrl -k $target
```

Save it as a 'showdesktop.sh' file, then make it executable (`chmod +x showdesktop.sh`) and finally assign it to the Win+D binding in the Shortcuts section of System Settings.

Locking the screen is an easier process: there's no need to wrap anything into a script; instead, using a plain command will be enough:

```sh
qdbus org/freedesktop/ScreenSaver /ScreenSaver org.freedesktop.ScreenSaver.SetActive True
```

## Custom keybindings

As a continuation of the previous step, we'll try to reproduce the behaviour of the Win+D and Win+L combinations, which will minimise all windows and lock the desktop respectively.

![](img/0fc17bd4c29dc437e3ac28a53f7559db_43_0.png)

## Built-in web browser

There is an abundance of browsers for Linux, but how about a browser right on your desktop? We've seen something similar in Ubuntu's Unity, but in KDE a mini-browser is implemented as a plasmoid, meaning it doesn't get in your way together with applications' windows and it sits quietly on the desktop. To add it: just right-click on the desktop and select the 'Add Widgets...' item, then search for 'Web browser'. Double-click to add it to the desktop and see the default www.kde.org page opening in a tiny window. The plasmoid doesn't have many settings except for a shortcut binding, so to change the website, type its address in the plasmoid's text entry field with the mandatory 'www.' prefix. The plasmoid will load your page and auto-adjust its layout to the size of the plasmoid itself — you can resize to make the page inside the plasmoid readable.

The web browser plasmoid currently uses the QtWebKit engine, the same as in the Firefox browser, but the KDE team plans to switch to the newer QtWebEngine, which is based on the Chromium code and renders pages much better. Still, the current plasmoid is very capable and has a decent score of 390 points on html5test.com.

![](img/0fc17bd4c29dc437e3ac28a53f7559db_44_0.png)

![](img/0fc17bd4c29dc437e3ac28a53f7559db_44_1.png)

## Launch single settings modules

All KDE Plasma 5 settings are conveniently grouped into the System Settings application, which can also be launched by calling upon the **systemsettings5** command. There is no denying that this application is very nice, but finding the perfect setting can take some time and you might want to access everything in a more elegant way. This can be done using the **kcmshell5** command. First, let's see what modules we have:

```sh
$ /usr/bin/kcmshell5 --list
```

Use any module as an argument to **kcmshell5** and it will then launch the respective single module without accessing the control panel. For example:

```sh
$ /usr/bin/kcmshell5 kwincompositing
```

... will launch the desktop compositor's setup. This technique lets you launch any module from the list and then, maybe, create a shortcut with such a command, or bind it with a keyboard shortcut. It is also possible to launch several modules with a single command. For instance:

```sh
$ /usr/bin/kcmshell5 mouse kcm_xserver
```

... will display a nice window with all these modules shown as different sections inside a single window.

For even more Plasma 5 tips and tricks, it's always worth paying a visit to the KDE wiki – community members are always uploading guides to [userbase.kde.org/Tutorials](http://userbase.kde.org/Tutorials).

> **Plasma 5 desktop is modular, so we can kill the shell without disturbing anything else, be it a background process or a graphical application**

## Uniform look

As far as we can remember, the first attempt to clear the visual differences between Qt-based and GTK-based apps was taken in Red Hat Linux 8.0 with the introduction of the Bluecurve theme. Nowadays, the problem is still present: modern GTK2 and GTK3 apps don't quite fit well into the KDE desktop. There are various workarounds for this issue, including the QtCurve theme, which works well for GTK2 but has poor support for GTK3. Another option is to use the Orion GTK theme, which looks similar to Plasma 5 Breeze (the default theme) but still has huge visual inconsistencies with it. Luckily, we have a working port of the Breeze theme to GTK at [github.com/dirkv1/gnome-breeze](https://github.com/dirkv1/gnome-breeze), covering both light and dark variants. Simply copy the theme into either `~/.themes` or `/usr/share/themes` and then select it in *System Settings* (*Widget style* -> *GNOME Application style* (*GTK*)). Now you have a consistent visual experience regardless of the graphical toolkit used.

![](img/0fc17bd4c29dc437e3ac28a53f7559db_45_0.png)

# Create user interfaces with MonoDevelop forms

Creating GTK-based UIs used to be an exercise in frustration, but MonoDevelop changes all that...

+   **Tim Hanna** has been in the IT business since the days of the Amiga PC. Serving as a journalist, tutor, speaker and author of scientific books, he has seen every aspect of the mobile market more than once

Working with GTK is a pain: its handle-function-driven coding paradigm might have looked cool in the time of Palm OS, but it looks hopelessly dated now.

V-CL has attempted to improve the situation by providing an object-oriented wrapper for most GUI classes. This led to more compact code, but it’s miles away from true RAD (rapid application development): seeing your user interface as you work on it is a true productivity booster. Visual Basic was always a leader in this respect. The very first version of the product ran under DOS, but it did not skimp on providing a WYSIWYG-GUI editor.

Even though Mono contains a runtime emulation for Microsoft’s Windows.Forms namespace, MonoDevelop’s WYSIWYG editor is based on GTK. Since that framework is just as cross-platform as Mono, using GTK should not be an issue for most desktop-based applications. Furthermore, many of the concepts discussed here can also be applied to a variety of other GUI tools.

MonoDevelop will produce a default GTK 2.0 project skeleton for you. In addition to the known C# files, our project now also comes with a folder containing a form layout and a resource file with a few icons. Actual program execution is still handled via `Program.cs`, which by default contains the following code:

```csharp
class MainClass
{
    public static void Main (string[] args)
    {
        Application.Init ();
        MainWindow win = new MainWindow ();
        win.Show ();
        Application.Run ();
    }
}
```

`Application.Init()` is a static method domiciled in the GTK framework’s main class. After creating and displaying a new instance of the `MainWindow` class, we invoke `Run()` in order to start the event loop.

## Resources

-   **MonoDevelop**
    -   [monodevelop.com](http://monodevelop.com)

Begin by firing up MonoDevelop. We covered the installation and deployment instructions in the first part of this C# and MonoDevelop series (issue #157). Then create a new project based on the template C# > Gtk 2.0 Project.

![](img/0fc17bd4c29dc437e3ac28a53f7559db_45_1.png)

Right: We’ll make a simple resistor colour code calculator this time

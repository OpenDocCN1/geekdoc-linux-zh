
## TUTORIALS Desktop switcheroo

![](img/5cfcf2f4448dccdd1c5c2a2851544557_67_0.png)

> When adding a few guides to Sway, the otherwise barren desktop becomes both nice to look at and informative.

When you start running these packages, you will find that they come with less features in order to make them slim. Saving on resources is the first priority, making it necessary to add simple elements on your own. Examples are the action bar and tiling methods. A window manager is very much a habit – break that habit and you must think carefully every time you want to do something. Fortunately, you’ll learn quickly when you switch to a new one. As you try new window managers, though, you end up guessing key combinations and setting everything to your liking. Tweak and what it looks like can take several attempts, so having your old window manager running while you do this is useful. In this tutorial, you will discover some simple ways to try out the Awesome and Sway window managers. To test Awesome, we need to nest an X session on top of what you are already running. Using Xephyr, you can achieve a likeliness and see what happens when you make changes. You can start Sway by running `sway`, which starts a nested Wayland session.

> Your biggest challenge will be keybindings – they tend to be the same on most systems. Being able to lock the keyboard input to the nested desktop is helpful.

### Dwl – compile your own.

As part of the Suckless (low-overhead design) tools, you can find `dwm`. This is a desktop environment that you can compile yourself. Any changes and tweaks are set in the `config.h` file before compiling. No changes are made during execution and you have no configuration files during normal operation.

The idea is to have everything set before you install the software, making the binaries small and efficient. It does make it necessary for users to be at least aware of methods for developing software. Dwl is a Wayland clone of that system. If you want to try it out, be prepared to handle patches and troubleshooting C code. To be able to build the software, you need to understand how to collect all dependencies for the software. Fortunately, dwl only requires two packages: `wroots` and `wayland-protocols`. Optionally, you may want also `xorg-wayland`; once installed, you need to enable it in `config.mk`.

For an experienced programmer, this is a simple task. Being a green hobby programmer, it is a great way to get started with the whole C/C++ development process. After your first tutorials, this is the way to actually learn the whole process.

Because the designer implemented only a few features, you need to use patches to get everything how you like. Put in the effort, though, and you can move on to your own projects. Once you have passed that hurdle, this is the slimmest desktop you could imagine.

Vital for the use of most window managers, and tiling ones in particular, is the Mod key. You combine this key with another to make things happen. Most common is to have Mod+key+Enter to open a terminal and Mod-key-d to get a menu. As you can probably can guess, this is the Super key in most setups. When testing it out, you may need to set your Mod-X-key to Mod1 to use the Alt key, because the Super key will be busy by your main window manager. The Super (or Windows) key is usually Mod4. The first time you start an application, you may find that it loads in your main window manager, not the nested one. This can happen if you are already running the application.

### Xcellent Xephyr

There are several ways to nest an Xorg desktop. You need a new X server to host your desktop and applications. Also, in Xorg, you need a DISPLAY variable set for your screen. Xpra is one, but the designers intended it for remote use, so in this case you use Xephyr. One reason for nesting your sessions is the complexity of settings you have. Another is the wide range of possibilities you have for tweaking your desktop. You need to keep track of your settings and try new ones on a trial and error basis. So, how do you go about this?

The best way is to create all your settings where they will end up when you choose to switch. You can then point to them as you start your new environment.

```
$ cd ~/.config/awesome/
$ Xephyr -5 -resizeable -screen 136x768 & sleep 1; DISPLAY=:5 awesome -c rc.lua
```

As you can see above, you are pointing directly to the configuration file. In the case of Awesome, you need to run in the directory where your other configuration files are usually. The `rc.lua` file is yours but if you fetch one from the web, the links are often local under the directory. They do not point to the global position – instead of `~/.config/awesome/themes/` you point to `themes/`.

This makes it simple to switch the entire configuration by changing the directory to another directory. Once you have found your own settings, you have to make small tweaks after you switch to use Awesome on your main system.

Even using the nesting system, you won’t cover all functions, so make sure you have a backup system for the first few times you run the new one. Be aware that you must also have the correct version of Lua installed because many configuration files point directly to those binaries. When the Xephyr command starts, you see a new window where the entire desktop shows up. You can lock the keys to the new applications, making it easier to experiment. With the Awesome window manager, you can reload the configuration with the key combo Alt+Ctrl+r, making it easy to edit and test repeatedly.

### Sway but simpler

Due to the design of Wayland, you can start a new desktop with ease whenever needed. In their work, the designers created the concept of different level compositors. These are: System, which runs from boot; Session, which runs a user's session; and Embedding, which runs small applications or even a single video from your browser.

You will use Sway as a session compositor, making it run nested under your running compositor. Once you decide to stay with Sway, you can make it your default from your display manager (GDM) where you login. Other options are available for special systems.

To control what you are doing, look for the configuration file in `~/.config/sway/config`. All of the configuration can be in this file or you can split it into files under `~/.config/sway/config.d`. Run Sway from the terminal:

```
$ sway -c ~/.config/sway/config
```

Sway opens like any other application and you can start new applications, which show up on your new desktop. The main reason for doing this, though, is to test the window manager. Play around with the shortcuts and see if the chosen keys suit you. Now, you can also set different configurations and hit Smot-Shift-c to reload the configuration. This way, you can quickly run through all your ideas while still having a stable main desktop. Here, again, you must be prepared to do more tweaks when you start running it as your main window manager. There will be small details in the configuration that may stop some features.

This is all well and good, but there is another case you may want to consider: when you want to run only one application all the time. When would that be? For embedded systems, such as your Raspberry Pi controlling your automation project. A smart home application that does not require Big Tech to know what you're doing is one example. A media player is another, perhaps connecting to your regular TV, giving you a smart home entertainment system.

Any small system you build with a single-board computer can run Linux. You wouldn't choose anything else, would you? All of them have a user interface, some of them even have their own screen. Such a system needs only the application it was meant for and nothing else.

Enter Cage, a tiny compositor for Wayland with a few twists. It only opens one window in full-screen mode and exits when that application stops. It also deliberately lacks screen controls and border decorations. All of this creates a system that doesn't have any tools that would be capable of doing damage to the system. In this way, the attack surface for hackers is much smaller.

The intention of this software is to make a small system called a kiosk. These systems are the ones where you buy tickets or search for local information or other public services. In such a system, you want only the particular application to run. Often this is written as a web page. In a public space, though, you want only the specific application to run. The safest way to do this is to start it using your initiation system.

Cage runs any application that you put as the first parameter. In the earlier mentioned scenario, the application is the only one started by your chosen system. Yes, Systemd is the industry standard but there are others!

![](img/5cfcf2f4448dccdd1c5c2a2851544557_68_0.png)

Keybindings in Awnesime, and other window managers, can be hard to remember. To get the reminder page, use 'Super-V'.

### Cagey desktops

To install Cage, you can use your package manager. If you like the inclination, the code is available on GitHub: https://github.com/hjilves/cage. Clone the repo and use `meson` to build it. Do that if you know how; for the rest of us, install with the `apt` command:

```
$ sudo apt install cage
```

Cage has very few options and they are for window dressing and when you need a dual-monitor config. The only thing you need to do is to choose the application and run it:

```
$ cage sway
```

You get the same window, the difference is below the surface; Cage is a compositor in itself, so you can run anything in it. You can use it to run apps remotely and have them show up on your desktop. Being a tiny binary, Cage is fast and efficient. The point is that you can lock a user in a 'cage', allowing a safer way to allow remote execution via Wayland and its remote back-end.

To run it remotely, it gets more complex. But not much. First, you must set values on the remote system for the wroots execution – this is described in the documentation. As the designers made Cage for the kiosk environment, the most interesting use of this software is single-application boxes.

When switching environment, you need to be aware of both the computer and yourself. The computer must be set up correctly and you must learn to make actions automatically. If you don't, you will waste a lot of time when you have more important things to do. With the right tools, you can run things over the network, too, and have one environment on each computer. 87

> **QUICK TIP**
> The easiest way to hop is between Wayland-based desktop environments. They nest on their own, while X11 requires special software to nest.

![](img/5cfcf2f4448dccdd1c5c2a2851544557_68_1.png)

In Awnesime, you get a nice list of errors when there are mistakes in the configuration file causing startup problems.

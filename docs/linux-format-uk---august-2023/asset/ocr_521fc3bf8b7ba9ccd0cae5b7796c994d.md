# TUTORIALS Desktop switcheroo

![](bbox=[0.05, 0.07, 0.55, 0.26])

> When adding a few guides to Sway, the otherwise barren desktop becomes both nice to look at and informative.

When you start running these packages, you will find that they come with less features in order to make them slim. Saving on resources is the first priority, making it necessary to add simple elements on your own. Examples are the action bar and tiling methods. A window manager is very much a habit – break that habit and you must think carefully every time you want to do something. Fortunately, you’ll learn quickly when you switch to a new one. As you try new window managers, though, you end up guessing key combinations and setting everything to your liking. Tweak and what it looks like can take several attempts, so having your old window manager running while you do this is useful. In this tutorial, you will discover some simple ways to try out the Awesome and Sway window managers. To test Awesome, we need to nest an X session on top of what you are already running. Using Xephyr, you can achieve a likeliness and see what happens when you make changes. You can start Sway by running `sway`, which starts a nested Wayland session.

> Your biggest challenge will be keybindings – they tend to be the same on most systems. Being able to lock the keyboard input to the nested desktop is helpful.

# Dwl – compile your own.

As part of the Suckless (low-overhead design) tools, you can find `dwm`. This is a desktop environment that you can compile yourself. Any changes and tweaks are set in the `config.h` file before compiling. No changes are made during execution and you have no configuration files during normal operation.

The idea is to have everything set before you install the software, making the binaries small and efficient. It does make it necessary for users to be at least aware of methods for developing software. Dwl is a Wayland clone of that system. If you want to try it out, be prepared to handle patches and troubleshooting C code. To be able to build the software, you need to understand how to collect all dependencies for the software. Fortunately, dwl only requires two packages: `wroots` and `wayland-protocols`. Optionally, you may want also `xorg-wayland`; once installed, you need to enable it in `config.mk`.

For an experienced programmer, this is a simple task. Being a green hobby programmer, it is a great way to get started with the whole C/C++ development process. After your first tutorials, this is the way to actually learn the whole process.

Because the designer implemented only a few features, you need to use patches to get everything how you like. Put in the effort, though, and you can move on to your own projects. Once you have passed that hurdle, this is the slimmest desktop you could imagine.

Vital for the use of most window managers, and tiling ones in particular, is the Mod key. You combine this key with another to make things happen. Most common is to have Mod+key+Enter to open a terminal and Mod-key-d to get a menu. As you can probably can guess, this is the Super key in most setups. When testing it out, you may need to set your Mod-X-key to Mod1 to use the Alt key, because the Super key will be busy by your main window manager. The Super (or Windows) key is usually Mod4. The first time you start an application, you may find that it loads in your main window manager, not the nested one. This can happen if you are already running the application.

# Xcellent Xephyr

There are several ways to nest an Xorg desktop. You need a new X server to host your desktop and applications. Also, in Xorg, you need a DISPLAY variable set for your screen. Xpra is one, but the designers intended it for remote use, so in this case you use Xephyr. One reason for nesting your sessions is the complexity of settings you have. Another is the wide range of possibilities you have for tweaking your desktop. You need to keep track of your settings and try new ones on a trial and error basis. So, how do you go about this?

The best way is to create all your settings where they will end up when you choose to switch. You can then point to them as you start your new environment.

```
`$ cd ~/.config/awesome/`
`$ Xephyr -5 -resizeable -screen 136x768 & sleep 1; DISPLAY=:5 awesome -c rc.lua`
```

As you can see above, you are pointing directly to the configuration file. In the case of Awesome, you need to run in the directory where your other configuration files are usually. The `rc.lua` file is yours but if you fetch one from the web, the links are often local under the directory. They do not point to the global position – instead of `~/.config/awesome/themes/` you point to `themes/`.

This makes it simple to switch the entire configuration by changing the directory to another directory. Once you have found your own settings, you have to make small tweaks after you switch to use Awesome on your main system.

Even using the nesting system, you won’t cover all functions, so make sure you have a backup system for the first few times you run the new one. Be aware that you must also have the correct version of Lua installed because many configuration files point directly to those binaries. When the Xephyr command starts, you see a new window where the entire desktop shows up. You can lock the keys to the new applications, making it easier to experiment. With the Awesome window manager, you can reload the configuration with the key combo Alt+Ctrl+r, making it easy to edit and test repeatedly.

# Sway but simpler

Due to the design of Wayland, you can start a new desktop with ease whenever needed. In their work, the designers created the concept of different level compositors. These are: System, which runs from boot;
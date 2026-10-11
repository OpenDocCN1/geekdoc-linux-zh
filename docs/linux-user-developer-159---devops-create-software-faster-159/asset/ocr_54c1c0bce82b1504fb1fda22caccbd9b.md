# Tutorial Plasma 5

# Make your perfect Plasma 5 desktop

![](bbox=[0.06, 0.26, 0.18, 0.37])

Alexander Iolstoy
has spent years fine-tuning his Linux system to make it blazingly fast, but he keeps on searching for more tweaks. This kind of addiction seems to be a good one.

Use hidden tricks to reveal the inner power of this bleeding-edge advanced desktop environment

The holy wars between KDE and Gnome users seem to be long over, perhaps because of a massive migration of the latter to Cinnamon, but many of the rest still love their KDE installation for being fast, configurable and feature-rich. But KDE 4, first released seven years ago, is moving aside to free the way for the shiny new Plasma 5, the next-generation hardware-accelerated desktop with a sleek modern look, yet retaining the much valued 'Swiss Army knife' approach, which always inspired KDE users and developers. Just like the aging KDE 4, Plasma 5 is a modular desktop made of plugins that can be rearranged in any way. The desktop itself is a converged shell, which adapts to different target devices on the fly. Together with modern Qt5-based applications, it makes the experience consistent and helps ensure the workflow is more elegant.

# Start and stop

The most obvious reason for restarting the graphical shell is applying settings that require more than just hitting the Apply button. Most people would simply log out and then log back in, but in this case all launched applications will be shut down, which is not preferable for many.

The Plasma 5 desktop is modular and it means that we can kill the shell without disturbing anything else, be it a background process or a graphical application. Open Konsolle, or maybe hit Alt+F2 to show up the KRRunner heads-up prompt, and type:

```
$ kquitapp5 plasmashell
```

... and then:

```
$ plasmashell
```

... to start it again. All of your running apps will remain up. While the shell is down you can still access KRrunner and even switch between applications by making use of the familiar Alt+Tab sequence.

# Resources

Plasma 5 desktop

The new Plasma 5 desktop may not yet be mature enough, but it's been closing the gap very quickly in the past months, so that many people already use it on a daily basis. Kubuntu, OpenSUSE, KaOS, Manjaro and many others offer fine-tuned distributions with Plasma 5 out of the box. The steps here cover tips and tricks that work for both KDE 4 and 5, though some are Plasma 5-specific.

![](bbox=[0.2, 0.63, 0.88, 0.88])

> Right: KDE Plasma 5 is perhaps the most customisable and theme-able desktop on Earth
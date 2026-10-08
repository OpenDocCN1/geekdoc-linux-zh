# Part II: Ubuntu for Desktop Users

# FIGURE 5-2:
Compiz window manager's Window Control menu

![](bbox=[0.105, 0.172, 0.598, 0.439])

All of these window controls are fairly standard and are found in the window decoration and title bar layouts used by most modern window managers. However, they are often found in different portions of the title bar and look very different. Ubuntu 10.04 introduced a new theme called Ambiance, which replaced the traditional brown Human theme that was used by all previous versions of Ubuntu. The Human theme features the window controls that are discusssed in this section in the more traditional upper-right portion of the title bar. Regardless of how you feel about them, you can always move the controls back to the right by executing the following command from GNOME Terminal or other command-line application.

```
gconftool-2 --set /metacity/general/button_layout \
-- type string minimize,maximize,close
```

You can put them back to their default position in the Ubuntu 10.04 Ambiance theme by reversing the command, as in the following example:

```
gconftool-2 --set /metacity/general/button_layout \
-- type string minimize,maximize,close:
```

# Menus in GNOME

As discussed earlier in this chapter, GNOME provides two different types of menus: menus located in a panel, which provide easy access to different applications, locations, and capabilities on your system; and context-sensitive menus that provide access to different capabilities
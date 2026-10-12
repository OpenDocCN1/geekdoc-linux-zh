# LISTING 4.2 Sample .xinitrc File

```
```text
# Sample .xinitrc file

# This .xinitrc file has configuration support for the following X11
# window managers: AnotherLevel, fvwm, fvwm2, KDE, twm, mlvm, AfterStep
                WindowMaker, wm2, wmx, mwm, GNOME
#
# Use AnotherLevel's configuration of the fvwm2 window manager
# fvwm2 -cmd 'FvwmM4 -debug /etc/X11/AnotherLevel/fvwm2rc.m4'
#
# Use fvwm2
# fvwm2
#
# Use fvwm
# fvwm
#
# Use the K Desktop Environment
startkde
#
# Use twm - note: no longer needs an X terminal started!
# twm
#
# Use the mlvm (Macintosh-like) window manager
# mlvm
#
# Use AfterStep
# afterstep
#
# Use WindowMaker
# exec wmaker
#
# Use the wm2 window manager
# wm2
#
# Use the wmx window manager
# wmx
#
# Use Motif's or LessTif's mwm
# mwm
#
# Use GNOME
# exec gnome-session
```
```

Note that the sample .xinitrc file in Listing 4.2 is currently set to use the K Desktop Environment. To use a different window manager (if installed on your system), add or remove the appropriate pound sign in the file; then use the startx command to start a new session:

```
```text
# startx
```
```
This large section combines several variables and loads the correct keymaps.

```
```bash
# run all system xinitrc shell scripts.
for i in /etc/X11/xinit/xinitrc.d/* ; do
    if [ -x "$i" ]; then
        . "$i"
    fi
done

# now, we see if xdm/gdm/kdm has asked for a specific environment
case $1 in
    xserver-geome)
        exec xterm -geometry 80x24-0-0
        ;;
    gdm)
        exec gdm
        ;;
    gnomesession)
        exec gnome-session
        ;;
    kde)
        exec startkde
        ;;
    *)
        # we assume that switchdesk is installed.
        exec /usr/share/apps/switchdesk/Xclients.anotherlevel
        ;;
    esac

# otherwise, take default action
if [ -x "$HOME/.xsession" ]; then
    exec "$HOME/.xsession"
elif [ -x "$HOME/.Xclients" ]; then
    exec "$HOME/.Xclients"
elif [ -x /etc/X11/xinit/Xclients ]; then
    exec /etc/X11/xinit/Xclients
else
    # should never get here; failsafe fallback
    exec xsm
fi
```
```

Finally, this section starts the appropriate desktop interface. If the system does not use one of the specified desktops, the `xsm` command is issued, which starts a basic X session.

# ## Xresources

The XDM login screen can be customized with the `Xresources` file that is referenced in the `Xsession` file. This file uses the standard `Xresource` format, which is discussed in more detail in the "Customizing X applications" section later in the chapter.

```
```text
! $XConsortium: Xresources /main/B 1996/11/11 09:24:46 svick $
xlogin*login.translations: #override
        Ctrl<Key>R: abort-display(\n)
```
```
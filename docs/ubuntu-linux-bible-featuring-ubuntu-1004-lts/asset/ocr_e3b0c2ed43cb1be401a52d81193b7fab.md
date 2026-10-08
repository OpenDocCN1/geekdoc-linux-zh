# Part II: Ubuntu for Desktop Users

FIGURE 5-40

Permanently changing Login Screen preferences

![](bbox=[0.098, 0.172, 0.672, 0.325])

Make the file executable (chmod 755 ~.session), and the next time that you log in your system, the system will automatically start the IceWM window manager (in this example) instead of the GNOME desktop. For compatibility with other ways of starting the X Window System, you should also create a symbolic link to this file called .xinitrc, also in your home directory. You would do this with a command like the following:

```
ln -s ~/session ~/.xinitrc
```

Experimenting with different window managers is fun because each represents someone's idea of how you "should" interact with a graphical system, start applications, and so on. I've been using the X Window System since version 10, and thus have burnt more time than I ever could calculate experimenting with, configuring, and customizing many of the window managers that have been written in the last 20+ years. But it's been fun.

# Tip

On low-memory, low-resource systems such as old laptops, you may want to start Linux without a graphical interface—if you do this, you can start the X Window System using a command such as startxinit, which will also pick up the X11 startup file and symbolic link that you just created, and will therefore start your window manager for you. ■

The previous instructions changed whether your Ubuntu runs GNOME or a window manager. However, as mentioned earlier, all Linux desktop systems run a window manager under the covers. By default, GNOME on Ubuntu runs Compiz, KDE runs KWin, and so on. If you still want to run GNOME but are interested in changing the window manager that it runs under you must run another window manager that conforms to the Inter-Client Communication

184
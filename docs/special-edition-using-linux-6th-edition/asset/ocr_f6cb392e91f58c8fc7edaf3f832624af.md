```
startkde
```

`/opt/kde/bin/startkde` runs the various applications required to provide the KDE environment.

# Exploring Startup of the X Window System

Each distribution has a slightly different startup sequence, and your startup sequence will also be different if you use gdm, GNOME, or another window manager. These sequences also tend to change from version to version of a distribution. Obviously trying to document all of the possible startup sequences would take us quite a while and make for rather boring reading.

Understanding why all these scripts are run will help you understand the startup sequence for any distribution. Learning a little shell scripting won't hurt either. Let's go through the startup sequence from an explorer's point of view.

# inittab

Startup of the X Window System will almost always start with `/etc/inittab`, if you've configured a graphical login. `inittab` is init's configuration file, and init is about the first thing to run during Linux startup. It is process number one and is the ultimate parent of every other process in the system.

One of the few things that is standardized among Linux startup sequences is the definition of run levels. Runlevel 5 is a graphical login. So if you want the X Window System to automatically start on boot-up, you need to set your default runlevel to 5.

Starting at the beginning of our exploration, we should verify the default runlevel by looking for the following line in `/etc/inittab`:

```
id:5:initdefault:
```

This tells us that the default runlevel is in fact 5. The other likely setting is 3, which is full multiuser mode.

Now that we know the starting runlevel, let's determine what processes init will run (this example happens to be a Red Hat system):

```
```text
$ grep 5 /etc/inittab
# 5 - X11
id:5:initdefault:
15:5:wait:/etc/rc.d/rc 5
pr:12345:powerwait:/sbin/shutdown -c "Power Restored; Shutdown Cancelled"
1:2345:respawn:/sbin/mingetty tty1
2:2345:respawn:/sbin/mingetty tty2
3:2345:respawn:/sbin/mingetty tty3
4:2345:respawn:/sbin/mingetty tty4
5:2345:respawn:/sbin/mingetty tty5
6:2345:respawn:/sbin/mingetty tty6
# Run xdm in runlevel 5
x:5:respawn:/etc/X11/prefdm -nodaemon
```
```

The id line indicates the default runlevel. The 15 line is what kicks off all the `/etc/rc.d/rc5.d` scripts. We'll get back to that moment. The pr line is for when power is restored
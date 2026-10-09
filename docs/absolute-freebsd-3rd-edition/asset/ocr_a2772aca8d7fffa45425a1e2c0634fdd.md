While you can install any userland components in a jail, all a jail requires is the base system. Grab the *base.txz* distribution set for your desired FreeBSD release and extract it in your jail’s root directory.

```
# tar -xpf base.txz -C /jail/mariadb
```

That’s a complete install of the base operating system. If you want additional distribution sets, such as the debugging symbols, extract them the same way.

If you’ve built your own FreeBSD base system, you can install it in the jail.

```
# cd /usr/src
# make installworld DESTDIR=/jail/mariadb
```

Jails also need supporting directories and assorted detritus created by the install process, but not by `make installworld`. The `make distribution` command creates those files. If you already have these directories and files, though, don’t rerun `make distribution`: it’ll overwrite any local changes. And don’t forget the `DESTDIR` setting, unless you like resetting the host’s configuration!

```
# make distribution DESTDIR=/jail/mariadb
```

You can also build a custom userland with only enough binaries for running a single program, much as you would for a traditionally chrooted program. For most of us, that’s too much work, but if you want to break out ldd(1) and go wild, don’t let me stop you.

Once you have a jail userland, tell FreeBSD about your jail in */etc/jail.conf*.

# ### /etc/jail.conf

Traditionally, FreeBSD configured jails in */etc/rc.conf*. This was clunky and unwieldy. While FreeBSD still supports *rc.conf* configuration of jails, I recommend using the more flexible */etc/jail.conf* instead. This file isn’t in UCL, although it looks like something UCL could support. Define
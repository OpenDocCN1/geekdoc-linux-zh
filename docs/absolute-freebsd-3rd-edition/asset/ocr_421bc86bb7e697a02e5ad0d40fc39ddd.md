```
WARNING: FreeBSD 11.0-RELEASE-p1 is approaching its End-of-Life date.
It is strongly recommended that you upgrade to a newer
release within the next 1 month.
```

If the release has gone past End of Life, the notice gets more . . . emphatic.

To install the downloaded files, run `freebsd-update install`:

```
# freebsd-update install
Installing updates... done.
```

If the update requires any more steps, you'll see them here. Reboot your system, and you'll see that you're running the newest patchlevel.

# ## Updating Releases

This FreeBSD 11.0-p12 machine is within a month of End of Life? Let's update it with `freebsd-update upgrade`. Specify the target release with the `-r` flag.

```
# freebsd-update -r 11.1-RELEASE upgrade
```

The hardest part of this is to remember that -RELEASE is part of the version name.

The upgrade will inspect your system and present its conclusions.

```
The following components of FreeBSD seem to be installed:
kernel/generic world/base world/lib32

The following components of FreeBSD do not seem to be installed:
kernel/generic-dbg world/base-dbg world/doc world/lib32-dbg

Does this look reasonable (y/n)? y
```

Remember the install process, when you selected FreeBSD components to set up on your new host? That's what freebsd-update is checking for. You could have added or removed components, though, so take a look at the list. If it looks right, hit `y` to continue.

The update will more carefully scrutinize the system, comparing all existing files to the new release, and then start downloading.
# Updating Jails

So you have umpteen bajillion jails on your host, each dedicated to performing its own task in perfect isolation. That’s grand, until you have to apply security patches to all of the hosts. If you’ve built your FreeBSD from source, you’ll need to install a new world in each jail. If you’re running releases, though, freebsd-update(8) (see Chapter 18) can handle jails.

You can’t use freebsd-update(8) *inside* a jail. The same things that isolate a jail from compromising the host system disallow some of the functionality freebsd-update(8) needs. Instead, you update the jail from the host.

Any time you need to update your system, update your host before updating your jails. The host must be running a version of FreeBSD equal to or newer than any jail.

Start by copying */etc/freebsd-update.conf* to an alternate file, such as */etc/jail-freebsd-update.conf*. Remove all components that aren’t installed on the jail. Jails don’t have kernels, and most of them don’t have source code, so you’ll probably wind up with an entry like this:

+   Components world

When you run freebsd-update(8), it checks the version of FreeBSD you’re running on. It does this by querying the kernel. If you have FreeBSD 12.0 jails on a FreeBSD 13.0 system, the update program gets confused, chokes, and dies with mysterious errors. You need freebsd-update to use the release installed in the jail, not the version the host is running. Use the `--currently-running` option to tell freebsd-update(8) what version the jail is running. You must use the jail’s release, including the patch level. While you could easily enough extract that information from the jail, I encourage you to let freebsd-update ask the jail what version it’s currently running. Do this by using jexec(8) to query the version of FreeBSD running in the jail.

You’ll also use the -b flag to tell freebsd-update(8) the directory the jail lives in.
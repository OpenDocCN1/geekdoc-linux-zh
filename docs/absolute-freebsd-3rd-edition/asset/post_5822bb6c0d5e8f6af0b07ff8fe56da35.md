
## Updating Jails

So you have umpteen bajillion jails on your host, each dedicated to performing its own task in perfect isolation. That’s grand, until you have to apply security patches to all of the hosts. If you’ve built your FreeBSD from source, you’ll need to install a new world in each jail. If you’re running releases, though, freebsd-update(8) (see Chapter 18) can handle jails.

You can’t use freebsd-update(8) *inside* a jail. The same things that isolate a jail from compromising the host system disallow some of the functionality freebsd-update(8) needs. Instead, you update the jail from the host.

Any time you need to update your system, update your host before updating your jails. The host must be running a version of FreeBSD equal to or newer than any jail.

Start by copying */etc/freebsd-update.conf* to an alternate file, such as */etc/jail-freebsd-update.conf*. Remove all components that aren’t installed on the jail. Jails don’t have kernels, and most of them don’t have source code, so you’ll probably wind up with an entry like this:

- Components world

When you run freebsd-update(8), it checks the version of FreeBSD you’re running on. It does this by querying the kernel. If you have FreeBSD 12.0 jails on a FreeBSD 13.0 system, the update program gets confused, chokes, and dies with mysterious errors. You need freebsd-update to use the release installed in the jail, not the version the host is running. Use the `--currently-running` option to tell freebsd-update(8) what version the jail is running. You must use the jail’s release, including the patch level. While you could easily enough extract that information from the jail, I encourage you to let freebsd-update ask the jail what version it’s currently running. Do this by using jexec(8) to query the version of FreeBSD running in the jail.

You’ll also use the -b flag to tell freebsd-update(8) the directory the jail lives in.

Here, I update the jail called *test*. The jail’s files are in /jail/test. I use a jexec(8) command in backticks to check the current FreeBSD version.

```bash
# freebsd-update -f /etc/jail-freebsd-update.conf -b /jail/test/ --currently-running `jexec -l test freebsd-version` fetch install
```

Once freebsd-update finishes running, restart your jail. It’s upgraded.

Many people have written scripts to run through /etc/jail.conf and upgrade all of their jails. If you have more than a couple jails, you find or write such a script.

## More Jail Options

You can customize jails in all sorts of ways. The jail(8) man page includes the current list of jail options, but here’s a few features I commonly use.

Rather than letting jail(8) assign jail IDs, you can assign each jail a permanent ID with the jid option.

```
jid=101;
```

The securelevel option lets you raise the securelevel (see Chapter 9) within a jail. The jail’s securelevel can never be lower than that of the host.

You can view a jail’s startup messages by manually running a /etc/rc with a jail command. That’s inconvenient for routine troubleshooting, though. Direct the jail’s console messages to a file with the exec.consolelog option.

```
exec.consolelog="$j/logs/$name.log";
```

In addition to mounting /dev, a jail can have its own fdescfs(5) and procfs(5) with the mount.fdescfs and mount.procfs options.

## Jailing Ancient FreeBSD

In my experience, the phrase *enterprise network* is synonymous with “we have lots of ancient stuff that nobody dares touch.” Jails can help you cope with some of these systems. In 2014, I worked at a company that ran a critical custom-built PHP and MySQL application on FreeBSD 4.10. I don’t know when this server was installed, but FreeBSD 4.11 came out in January 2005, so: before then. This application used ancient versions of Perl, PHP, OpenSSL, and more.

Worse, this application lived on a repurposed desktop machine. With a standard-issue, high-quality desktop hard drive. I hid a spare desktop machine of the same vintage under my desk, just so I had a hope of getting FreeBSD 4.10 onto it. The most proper solution was to rewrite or replace this application. Several sysadmins had faced that task—and failed. I decided to virtualize it. FreeBSD 4.10 doesn’t run well on VMware—yes, you can find de(4) and fxp(4) drivers, but they’re for versions of those cards over a decade old. Here’s how I got this ancient FreeBSD system into a jail.

Drop to single-user mode. Unmount */proc*—yes, FreeBSD 4 still used */proc*. Those were the days. Tar up the entire filesystem, including temporary directories, like */usr/obj*, */usr/ports*, */var/tmp*, and suchforth. By modern standards, they won’t use much space at all, and you have no way to know what files you might need later. You can probably find an old PHP 5.0.whatever tarball out on the internet, but that would involve work.

Copy the tar file to your jail host and extract it in your jail directory.

```bash
# tar -C /jail/oldserver -xvpf oldserver.tgz
```

Be sure to use the -p flag to preserve permissions.

Now look at /etc/rc.conf. The jail host will handle all networking functions, so turn off any statements that set IP addresses or set routes. Get rid of daemons that provide services the jail host offers, such as time, packet filters, and SSH. Your jailed host needs only the functions that directly support the application. In this case, I needed Apache and MySQL.

Consider the jail's /etc/fstab. Do you need a NFS filesystem or some other special mount? Remove everything you don't need. If this application needs /proc, provide it with the jail option mount.procfs.

Remove the old /dev. You can't use FreeBSD 4 device nodes on a modern FreeBSD.

Configure the host to protect the jail. While people can write perfectly fine applications in Apache and PHP, not even the most ardent Apache and MySQL fan would encourage you to expose 15-year-old versions of these servers to the internet. Use the host's packet filter to protect the jail. Don't even consider using the migrated host's OpenSSH server.

You won't be able to use some FreeBSD 4 commands inside the jail, as the interfaces have diverged too far. A FreeBSD 4 ps(1) can't successfully query a modern FreeBSD kernel. You can copy statically linked versions of most of those programs from the host's /rescue and copy them into the jail, however.

Is it this simple? No, not really. The older the source system is, the more problems you'll have. Most of the problems I had in this particular migration meant changing a configuration file to account for the new underlying filesystem. You'll need to perform your usual sysadmin debugging. But it's one way to get a modern network interface on a system lacking a device driver for it, and it's the only way to get ZFS on a FreeBSD 4 system.

## Last Jail Notes

People have evolved many ways of using jails. Fully covering all of these features would pretty much require a book of its own, but here are some pointers.

You can use ZFS features to delegate a dataset entirely to the jail administrator so that jail owners can take their own snapshots and create their own child datasets. With the VIMAGE kernel option, you can give a jail its own routing table. If you're brave, nullfs(5) lets you recycle an operating system install and minimize disk utilization. You can establish per-jail resource limits with the RCTL kernel option.

If you have many jails, you might prefer using a jail management program, such as iocage or ezjail. Both are available in the Ports Collection.

Successfully using jails requires automating your maintenance. Each jail requires separate security patches, both for the userland and for installed packages. The more you can automate this process, the more likely it is that you'll actually perform such maintenance. I recommend using Ansible's jail modules or at least writing your own shell script to apply patches.

The jail(8) command will let you modify, create, and destroy jails without a command line. If you're doing extensive jail work, definitely read the man page.

Now let's look at some of FreeBSD's less well-known corners.

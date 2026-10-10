
You can set the script to be on (to activate it), off (to deactivate it), or reset (to set it to its default value).

If you've added a startup script to the main SysV startup script directory, you can have chkconfig register it and add appropriate start and stop links in the runlevel directories. When you do this, chkconfig inspects the script for special comments to indicate default runlevels. If these comments are in the file and you're happy with the suggested levels, you can add it to these runlevels with a command like this:

```
# chkconfig --add nfs-common
```

This command adds the nfs-common script to those managed by chkconfig. You would, of course, change nfs-common to your script's name. This approach may not work if the script lacks the necessary comment lines with runlevel sequence numbers for chkconfig's benefit.

## Managing Runlevel Services with ntsysv

The ntsysv utility is an interactive text-mode tool. It was created by Red Hat and is used mainly on Red Hat and related distributions, such as Fedora and Mandriva. If you run ntsysv without any arguments, you can configure your current runlevel. If you want to specify alternate runlevels to configure, run it with the `--level` option, as in `ntsysv --level 1` to configure runlevel 1 or `ntsysv --level 23` to configure runlevels 2 and 3. In either event, the result resembles Figure 5.2, which shows ntsysv running in an xterm window.

**FIGURE 5.2** The ntsysv program enables you to control services from a menu of available services.

![](img/f339a9f48c4b443e61c74acb4c9c3da4_305_0.png)

To adjust services, use your keyboard's arrow keys to select a service, and press the spacebar to toggle the service on or off. An asterisk in the square brackets indicates that the service is on. No asterisk means the service won't execute for the runlevels you've selected. When you're done, press the Tab key to highlight the OK button, and then press the Enter key.

## Checking Your Runlevel

Sometimes it's necessary to check your current runlevel. Typically, you'll do this prior to changing the runlevel or to check the status if something isn't working correctly. Two different runlevel checks are possible: checking your default runlevel and checking your current runlevel.

### Checking and Changing Your Default Runlevel

You can determine your default runlevel by inspecting the `/etc/inittab` file with the `less` command or opening it in an editor. Alternatively, you may use the `grep` command to look for the line specifying the `initdefault` action. On a Fedora system, you'll see something like this:

```
# grep :initdefault: /etc/inittab
id:5:initdefault:
```

On Debian, you'll probably see this:

```
# grep :initdefault: /etc/inittab
id:2:initdefault:
```

You may notice that neither system defines a process to run. In the case of the `initdefault` action, the process field is ignored.

If you want to change the default runlevel for the next time you boot your system, edit the `initdefault` line in `/etc/inittab` and change the runlevel field to the value that you want. If your system lacks an `/etc/inittab` file, create one that contains *only* an `initdefault` line that specifies the runlevel you want to enter by default.

### Determining Your Current Runlevel

If your system is up and running, you can determine your runlevel information with the `runlevel` command:

```
# runlevel
N  2
```

The first character is the previous runlevel. When the character is N, this means the system hasn't switched runlevels since booting. It's possible to switch to different runlevels on a running system with the `init` and `telinit` programs, as described next. The second character in the `runlevel` output is your current runlevel.

### Changing Runlevels on a Running System

Sometimes you may want to change runlevels on a running system. You might do this to get more services, such as going from a console to a graphical login runlevel, or to shut down or reboot your computer. This can be accomplished with the `init` (or `telinit`), `shutdown`, `halt`, `reboot`, and `poweroff` commands.

## Changing Runlevels with `init` or `telinit`

The `init` process is the first process run by the Linux kernel, but you can also use it to have the system reread the `/etc/inittab` file and implement changes it finds there or to change to a new runlevel. The simplest case is to have it change to the runlevel you specify. For instance, to change to runlevel 1 (the runlevel reserved for single-user or maintenance mode), you would type this command:

```
# init 1
```

To reboot the system, you can use `init` to change to runlevel 6 (the runlevel reserved for reboots):

```
# init 6
```

A variant of `init` is `telinit`. This program can take a runlevel number just like `init` to change to that runlevel, but it can also take the `Q` or `q` option to have the tool reread `/etc/inittab` and implement any changes it finds there. Thus, if you’ve made a change to the runlevel in `/etc/inittab`, you can immediately implement that change by typing `telinit q`.

![](img/f339a9f48c4b443e61c74acb4c9c3da4_307_0.png)

> The man pages for these commands indicate slightly different syntaxes; but `telinit` is sometimes a symbolic link to `init`, and in practice `init` responds just like `telinit` to the `Q` and `q` options.

## Changing Runlevels with `shutdown`

Although you can shut down or reboot the computer with `init`, doing so has some problems. One issue is that it’s simply an unintuitive command for this action. Another is that changing runlevels with `init` causes an immediate change to the new runlevel. This may cause other users on your system some aggravation because they’ll be given no warning about the shutdown. Thus, it’s better to use the `shutdown` command in a multi-user environment when you want to reboot, shut down, or switch to single-user mode. This command supports extra options that make it friendlier in such environments.

The `shutdown` program sends a message to all users who are logged into your system and prevents other users from logging in during the process of changing runlevels. The `shutdown` command also lets you specify when to effect the runlevel change so that users have time to exit editors and safely stop other processes they may have running.

When the time to change runlevels is reached, `shutdown` signals the `init` process for you. In the simplest form, `shutdown` is invoked with a time argument like

```
# shutdown now
```

This changes the system to runlevel 1, the single-user or maintenance mode. The `now` parameter causes the change to occur immediately. Other possible time formats include `hh:mm`, for a time in 24-hour clock format (such as `6:00` for 6:00 am or `13:30` for 1:30 pm), and `+m` for a time `m` minutes in the future.

You can add extra parameters to specify that you want to reboot or halt (that is, power off) the computer. Specifically, `r` reboots the system, `H` halts it (terminates operation but doesn’t power it off), and `P` powers it off. The `h` option may halt or power off the computer, but usually it powers it off. For instance, you can type `shutdown -r +10` to reboot the system in 10 minutes.

To give people some warning about the impending shutdown, you can add a message to the end of the command:

```
# shutdown -h +15 "system going down for maintenance"
```

If you schedule a shutdown but then change your mind, you can use the -c option to cancel it:

```
# shutdown -c "never mind"
```

### Changing Runlevels with the halt, reboot, and poweroff Commands

Three additional shortcut commands are `halt`, `reboot`, and `poweroff`. (In reality, reboot and poweroff are usually symbolic links to `halt`. This command behaves differently depending on the name with which it’s called.) As you might expect, these commands halt the system (shut it down without powering it off), reboot it, or shut it down and (on hardware that supports this feature) turn off the power, respectively.

In Exercise 5.1, you’ll experiment with some of the methods of changing runlevels just described.

#### EXERCISE 5.1

**Changing Runlevels**

This exercise will demonstrate the effects of changing the runlevel in various ways on a working system. Be aware that some of the effects will be different from one system to another, depending on both the distribution and the system-specific configuration of the computer. Also, in the course of running this exercise, you’ll reboot the computer, so you shouldn’t do it on a system that anybody else is using. To manage your runlevels, follow these steps:

- Log in as root, or acquire root privileges by using `su` or by using `sudo` with each of the following commands. Use a text-mode or remote login; some of the exercise activities will shut down X.
- Type `runlevel` to learn your current runlevel. Recall that the first character returned refers to the previous runlevel (N denotes no previous runlevel; it hasn’t been changed since the system booted). The second output character is the current runlevel. This is likely to be 2 on Debian or Debian-derived systems, and 3 or 5 on Red Hat or Red Hat-derived systems.

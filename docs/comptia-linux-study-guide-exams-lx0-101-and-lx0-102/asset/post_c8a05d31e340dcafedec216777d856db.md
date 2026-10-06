
## Chapter 5 • Booting Linux and Editing Files

The /etc/inittab file is one SysV feature that may not be used by newer startup systems, such as Upstart and systemd. Ubuntu 12.04, uses Upstart, provides no /etc/inittab at all. Fedora 17, which uses systemd, provides an /etc/inittab file containing nothing but noting its obsolescence. OpenSUSE 12.1 is also based on systemd, and it provides an /etc/inittab file, but it's no longer used in any way. Other distributions, such as Debian, continue to use SysV, and the exam continues to emphasize SysV (including /etc/inittab).

## Basic of the /etc/inittab File

Entries in /etc/inittab follow a simple format. Each line consists of four colon-delimited fields:

```
id:runlevels:action:process
```

Each of these fields has a specific name:

**Identification Code** The id field contains a sequence of one to four characters that identifies its function.

**Applicable Runlevels** The runlevels field contains a list of runlevels for which this entry applies. For instance, 345 means the entry is applicable to runlevels 3, 4, and 5.

**Action to Be Taken** Specific codes in the action field tell init how to treat the process. For instance, wait tells init to start the process once when entering a runlevel and wait for the process's termination, and respawn tells init to restart the process whenever it terminates (which is great for login processes). Several other actions are available;; consult the man page for inittab details.

**Process to Run** The process field is the process to run for this entry, including any options and arguments that are required.

The part of /etc/inittab tells init how to handle each runlevel looks like this:

```
10:0:wait:/etc/init.d/rc 0
11:1:wait:/etc/init.d/rc 1
12:2:wait:/etc/init.d/rc 2
13:3:wait:/etc/init.d/rc 3
14:4:wait:/etc/init.d/rc 4
15:5:wait:/etc/init.d/rc 5
16:6:wait:/etc/init.d/rc 6
```

These lines start with codes that begin with an l (a lowercase L, not a number 1) followed by the runlevel—for instance, 10 for runlevel 0, 11 for runlevel 1, and so on. These lines specify scripts or programs to be run when the specified runlevel is entered. In this case of example, all the scripts are the same (/etc/init.d/rc), but the script passes the runlevel number as an argument. Some distributions call specific programs for certain runlevels, such as shutdown for runlevel 0.

## Dealing with Runlevels and the Initialization Process

The upcoming section "Checking and Changing Your Default Runlevel" describes how to tell init what runlevel to enter when the system boots.

The /etc/init.d/rc or /etc/rc.d/rc script performs the crucial task of running all the scripts associated with the runlevel. The runlevel-specific scripts are stored in /etc/rc.d/rc7d, /etc/init.d/rc7d?, /etc/rc.d?, or a similar location. (The precise location varies between distributions.) In all these cases, is it a runlevel? When entering a runlevel, rc passes the start parameter to all the scripts with names that begin with a capital S and passes the stop parameter to all the scripts with names that begin with a capital K. This SysV startup scripts start or stop controls whether they're started or stopped when a runlevel is entered. These scripts are also numbered, in S10network and K355mb.

The program runs scripts in numeric order. This enables distribution designers to control the order in which scripts run by giving them appropriate names. Control is important because some services depend on others. For instance, network servers must be started after the network is brought up.

In reality, the files in the SysV run directories are symbolic links to the main scripts, which are typically stored in /etc/rc.d, /etc/init.d, or /etc/rc.d.init (again, the exact location depends on the distribution). These original SysV startup scripts have names leading the S or K name, and as sm instead of K355mb.

You can also start services by hand. With the start option, in /etc/init.d/smb start to start the smb (Samba) server. Other useful options are, restart, and status. Most scripts support all these options.

In which services are active in a runlevel, search the SysV startup script directory for filenames that begin with an S. Alternatively, you can use a runlevel management tool, as described next.

Distributions based on Upstart and often provide startup scripts that are named and work much like SysV-based systems; however, when the computer boots, it may use other startup methods, as described later, in "Using Alternative Boots." SysV scripts are provided mainly for backward compatibility to help system administrators who are familiar with the SysV startup method and for the benefit of administrative scripts that might rely on SysV scripts. Fedora is not in that (at least of Fedora 17); you may need to use native systemd methods rather than SysV if you use Fedora.

## Managing Runlevel Services

The SysV startup scripts in the run directories are symbolic links to the original script. This is done so you don't need to copy the script into each runlevel directory.

Instead, you can modify the original script without having to track its copies in all the SysV runlevel directories. You can also modify programs are active in a runlevel by editing the link filenames. Numerous utility programs are available to help manage these links, such as chconfig, update-rc.d, and rc-update. I describe the first of these tools because it's supported on many distributions. If your distribution doesn't support these tools, you should check distribution-centric documentation. These tools may provide impaired functionality on systems that don't use SysV; you may need to locate Upstart; or systemd-specific tools instead.

To list the services and their applicable runlevels like with chconfig,--list option. The output looks like this is likely to be much clearer:

```
# chconfig --list
pcmcia      0:off 1:off 2:on  3:on  4:on  5:on  6:off
nfs-common  0:off 1:off 2:off 3:on 4:on 5:on  6:off
xprint      0:off 1:off 2:off 3:off 4:on 5:on  6:off
seterial   0:off 1:off 2:off 3:off 4:off 5:off 6:off
```

This output shows the status of the services in all runlevels. For instance, you can see that nfs-common is inactive in runlevels 0–2, active in runlevels 3–5, and inactive in runlevel 6.

If you're in a specific service, you can specify its name:

```
# chconfig --level nfs-common
nfs-common  0:off 1:off 2:off 3:on 4:on 5:on  6:off
```

To modify the runlevels in which a service runs, you can use a command like this:

```
# chconfig --level 23 nfs-common
```

> The previous example is for Debian-based systems. On Red Hat-based systems, you would likely need to use chconfig instead.

You can set the runlevel to (to activate it), off (to deactivate it), or reset (to its value). If you want to change the default runlevel for the next time you boot your system, edit the initdefault line in /etc/inittab and change the runlevel field to the value you want. If your system lacks an /etc/inittab file, create one that contains only an initdefault line that specifies the runlevel you want to enter by. If your system doesn't use SysV, you'll need to adjust the default runlevel in some other way, as described in "Using Alternative Boot Systems."

## Checking Your Runlevel

Sometimes it's necessary to check your current runlevel. Typically, you'll do this prior to changing runlevel or to check the status if something isn't working. Two different runlevels are possible: checking your default runlevel and checking current runlevel.

## Checking and Changing Your Default Runlevel

On a SysV-based system, you can determine your default runlevel by inspecting the /etc/inittab file with less. Alternatively, you may use the grep command to look for the line specifying the initdefault action. On a Debian system, you'll see something like this:

```
# grep initdefault:/etc/inittab
id:2:initdefault:
```

If grep returns nothing, you've either mistyped or your computer is using Upstart, or some other initialization tool. On some systems, the second colon-delimited field will contain a 3, 5, or some value other than the 2

## Determining Your Current Runlevel

If your system is up and running, you can determine your runlevel information with the runlevel command:

```
# runlevel NN 2
```

The first character is the previous runlevel. When the character is N, this means the system hasn't switched runlevels since booting. It's possible to switch to different runlevels on a running system with the init and telinit programs, as described next. The second character in the runlevel output is your current runlevel.

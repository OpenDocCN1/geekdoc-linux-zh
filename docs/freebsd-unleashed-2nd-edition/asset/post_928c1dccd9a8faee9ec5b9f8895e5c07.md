
## The /etc/defaults/rc.conf File

Whether in FreeBSD 5.0 or in earlier versions, the resource configuration scripts are controlled by the same global configuration files: /etc/defaults/rc.conf, /etc/rc.conf, and the local rc.d directory tree. Everything else (all the other /etc/rc.* files or the contents of /etc/rc.d) should be left untouched so that future installations of FreeBSD can upgrade the files while preserving your customizations.

Take a look through the /etc/rc script. You’ll see that it’s completely automated; it works by checking whether certain variables are defined that control system configuration or whether certain files exist. If those variables or files are present, it executes a predefined, abstracted launch loop, which takes its parameters from those variables and files. Nothing in /etc/rc itself should be edited. In other systems, the system startup process is altered and extended by making changes to the resource configuration scripts themselves; in FreeBSD, though, the model is to automate and abstract as much as possible of the process and centralize the control files that specify the parameters.

In earlier versions of FreeBSD, there was only /etc/rc.conf. It contained all the variables that /etc/rc and related scripts would need in their default states, and any modifications to the system would be made to that file. This arrangement quickly became unmanageable, as the list of variables grew and the role of the file expanded. An administrator upgrading the system would painstakingly have to merge the old rc.conf with the new one—hardly an improvement over just editing /etc/rc in the first place.

Therefore, the solution was to create a directory called /etc/defaults and put a copy of rc.conf, with all the defaults filled in, into it. Now, /etc/rc.conf still exists, but the system will boot even if this directory is empty. Its purpose is to fill in overrides for the defaults in /etc/defaults/rc.conf. Typical overrides are for the networking configuration (IP address, hostname, gateway address, and so on) and for running daemons such as sendmail and sshd.

Let’s look at a typical block in /etc/defaults/rc.conf, as shown in Listing 10.1.

### Listing 10.1 Excerpt from /etc/defaults/rc.conf

```
# named. It may be possible to run named in a sandbox, man security for
# details.
#
named_enable="NO"                 # Run named, the DNS server (or NO).
named_program="named"             # path to named, if you want a different one.
named_flags=""                    # Flags for named
#named_flags="-u bind -g bind"    # Flags for named
```

Now, you can find what /etc/rc will do by default. In this case, the default behavior is to not run named at all.

Typically, variables in `/etc/defaults/rc.conf` are grouped into these blocks, with similar prefixes keeping them related and with a single “YES”/“NO” variable serving as a “master switch” at the top. If the variable is set to “NO”, generally none of the rest of the variables will matter; if it is set to “YES”, all variables apply unless commented out. The second `named_flags` line in the listing is provided as an example in case you want to create a bind user and group for named to run as.

## The /etc/rc.conf File

Let’s say you do want to run named. In the simplest case, all you have to do is edit `/etc/rc.conf` (the “overrides” file) and add the following line anywhere in the file:

```
named_enable="YES"
```

The rest of the `named_*` variables in `/etc/defaults/rc.conf` do not need to be copied into the overrides file. Remember, every variable in the “defaults” file is loaded into memory by `init`, and they only matter if the “master switch” for that block has been turned to “YES”. In that case, the variables will be used in the execution loop in `/etc/rc` to launch whatever process is controlled by the block you’re working on (in this case, named).

> **CAUTION**
> 
> As you tinker with `/etc/rc.conf`, it’s a very good idea to keep a backup copy on hand so that you can easily back out to a known working system configuration. Create a backup file by simply copying your existing file before you begin working on it:
> 
> ```
> # cp /etc/rc.conf /etc/rc.conf.revert
> ```

To switch back to the backup version, copy or move (rename) it back to its original name:

```
# mv /etc/rc.conf.revert /etc/rc.conf
```

You can use these other variables for fine-tuning, though, and override them just as easily. Let’s say your name server program is a customized version called `mynamed`. Let’s also say that you’ve created a `bind` user and group, intending that the name server should run as this user and group so it won’t be susceptible to as many security hacks. To handle that, all you need to do (assuming that `mynamed` has the same behavior and command-line options as `named`) is add these two lines to `/etc/rc.conf`:

```
named_program="mynamed"
named_flags="-u bind -g bind"
```

Just for curiosity’s sake, you can find out what `init` is doing with these variables:

```
# grep "named_enable" /etc/rc*
```

/etc/rc.network:

```bash
    case ${named_enable} in
```

Okay, so the named program is launched from /etc/rc.network. Looking in that file, you find this loop:

```
 network_pass2() {
 echo -n ' Doing additional network setup:'
 case ${named_enable} in
 [Yy][Ee][Ss])
 echo -n ' named'; ${named_program:-named} ${named_flags}
 ;;
 esac
```

Here, you can see all the named_* variables from both rc.conf files being invoked. Now, when you boot the system and see named appear in the console messages after “Doing additional network setup:,” you know that it’s applying your overrides over the defaults and running the name server automatically.

> **NOTE**
> See Chapter 12, “Shell Programming,” for a tutorial on shell scripting, which will help you in reading the resource configuration scripts.

The most typical variables that appear in /etc/rc.conf are the TCP/IP configuration parameters. Because these are different for every system, FreeBSD can’t very well specify them in the defaults. Listing 10.2 shows a typical /etc/rc.conf just after a new FreeBSD installation.

### Listing 10.2 A Newly Installed /etc/rc.conf

```
# This file now contains just the overrides from /etc/defaults/rc.conf
# please make all changes to this file.

# Enable network daemons for user convenience.
# -- sysinstall generated deltas -- #
kern_securelevel="1"
kern_securelevel_enable="YES"
linux_enable="YES"
sendmail_enable="YES"
sshd_enable="YES"
portmap_enable="NO"
nfs_server_r_enable="NO"
inetd_enable="NO"
network_interfaces="fxp0 100"
ifconfig_fxp0="inet 10.6.7.101 netmask 255.0.0.0"
defaultrouter="10.6.1.1"
hostname="freebsd1.testnetwork.com"
usbdo_enable="YES"
```

Some of these variables are, in fact, redundant with the defaults file; still, it can be useful to have them in the overrides file, as well, because many of these features (such as the NFS server) now have a one-turn toggle control, as it were.

Many programs, when you install them, will have to install a way for themselves to start up at boot time; /etc/rc.conf is not, however, the place for these programs. This file is supposed to be touched only by you, the administrator, and by the sysinstall program when it makes changes to the core system. Another structure, the /usr/local/etc hierarchy, is in place for the startup scripts and configuration files of user-installed programs (ports and packages) and for any scripts that /etc/rc and friends do not know about.

## The /usr/local/etc and /usr/local/X11R6/etc Directories

As you learned in Chapter 8, anything installed by the administrator goes into /usr/local. This is as true of startup scripts as it is of programs and shared libraries. The /usr/local/etc directory is the “local” equivalent of /etc (local referring to “this specific machine” as opposed to the generic components and settings found on all FreeBSD machines), and into it go all the configuration files installed by programs that you choose to install, rather than the ones controlled by the FreeBSD base system distribution.

> **NOTE**
> 
> It’s important to note that the difference between the /etc files and the /usr/local/etc files is not that the former are noneditable and the latter are editable. Just as most of the files in /etc should not be tampered with, many of the ones in /usr/local/etc also contain no user-serviceable parts or are designed not to need any modification by you in order to function (although the directory also contains customizable configuration files for installed programs). The distinction is that /etc controls the base system—for example, only those programs that are always part of a FreeBSD installation. The files in /usr/local/etc control programs that you install after the fact, from the ports collection or from packages (which you’ll learn about in Chapter 14, “Installing Additional Software”). /usr/local/etc also doubles as the location for any startup scripts you write.

The main local configuration directory, /usr/local/etc, contains configuration files that administrators edit to tune their programs’ behaviors. You learn more about configuring ports and packages in Chapter 14. Here, however, we’re interested in the rc.d (resource configuration for daemons) subdirectory.

init turns its attention to /usr/local/etc/rc.d after it has run through all the other /etc/rc.* or /etc/rc.d scripts. Any executable files within the directory that end in .sh are executed in lexicographical order. Examples of files that are installed in here include

![](img/48eec858cce7dfb89da36a4d40b7daf3_256_0.png)

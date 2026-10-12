
## 10.4. USER AUTHENTICATION WITH PAM

If *if* it exists. The second causes them to be asked for a password and the password checked. The third checks to see if the file */etc/nologin* exists, and if it does, displays the contents of the file, and if the user is not root, does not let them log in.

Note that all three modules are checked, *even if the first module fails*. This is a security decision—it is designed to not let the user know why their authentication was disallowed, because knowing why it was disallowed might allow them to break the authentication more easily.

The fifth line causes any necessary accounting to be done. For example, if shadow passwords have been enabled, the *pam_unix_acct.so* module will check to see if the account has expired, or if the user has not changed his or her password and the grace period for changing the password has expired.

The sixth line specifies that if the login program changes the user’s password, it should use the *pam_unix_passwd.so* module to do so. (It will do so only if an *auth* module has determined that the password needs to be changed—for example, if a shadow password has expired.)

The final line specifies that the *pam_unix_session.so* module should be used to manage the session. Currently, that module doesn’t do anything; it could be replaced (or supplemented—not only *auth* modules can be stacked) by any necessary module.

While the order of the stanzas in */etc/pam.conf* doesn’t matter, the order of the lines within a stanza may. (Actually, the order of the lines for each *service type*/*module type* pair is what matters.) While it doesn’t really matter much in which order *required* modules are called, there are other *control flags* available. While *optional* is rarely used, and never used by default on a Red Hat Linux system, *sufficient* causes order to become important.

Let’s look at the *auth* configuration for *rlogin*:

```
rlogin  auth  required      /lib/security/pam_security.so
rlogin  auth  required      /lib/security/pam_nologin.so
rlogin  auth  sufficient   /lib/security/pam_rhosts_auth.so
rlogin  auth  required     /lib/security/pam_unix_auth.so
```

¹Future versions of PAM will allow you to specify different behavior; the standard is in the process of revision.

That looks *almost* like the login entry, but there’s an extra line specifying an extra module, and the modules are specified in a different order.

First, `pam_security.so` keeps root logins from happening on insecure terminals. This effectively disallows all root login attempts. If you wish to allow them (in which case we recommend that you either not be internet-connected or be behind a good firewall), you can simply remove that line.

Second, `pam_nologin.so` checks `/etc/nologin`, as specified above.

Third, if `pam_rhosts_auth.so` authenticates the user, PAM immediately returns success to rlogin without any password checking being done. If `pam_rhosts_auth.so` fails to authenticate the user, that failed authentication is ignored.

Finally (if `pam_rhosts_auth.so` has failed to authenticate the user), normal unix password authentication is performed.

### 10.4.4 The Default Stanza

When packages containing applications which use PAM are installed, they automatically add stanzas to `/etc/pam.d`. Whenever possible, they don’t specify what modules to use—they just copy whatever has been put in the DEFAULT stanza near the top of `/etc/pam.conf`. By changing that stanza, you can change the default entries used by most applications. If you do this, you will need to check `/etc/pam.conf` after you add new PAM-aware applications to make sure that the stanza that was added fits your system.

### 10.4.5 Shadow Passwords

The default `pam_unix.*.so` modules can support shadow passwords. In order to convert your system to shadow passwords, use these commands:

```
cd /etc
pwconv
chmod 600 passwd- shadow-
```

The `pam_unix.*.so` modules will automatically detect that you are using shadow passwords and make all necessary adjustments.

### 10.4.6 More Information

This is just an introduction to PAM. More information is included with the system in `/usr/doc` in text, HTML, and PostScript format, including a *System Administrators’ Guide*, a *Module Writers’ Manual*, an *Application Developers’ Manual*, and the PAM standard, DCE-RFC 86.0. In addition, documentation is available from the Red Hat web site, at http://www.redhat.com/linux-info/pam/

## 10.5 The Boot Process, Init, and Shutdown

### 10.5.1 System V Init

This section is a brief description of the internals of the boot process. It basically covers in detail how the machine boots using SysV Init and the differences between the original init used in older Linux releases.

Init is the program that gets run by the kernel at boot time. It is in charge of starting all the normal processes that need to run at boot time. These include the gettys that allow you to log in, NFS daemons, FTP daemons, and anything else you want to run when your machine boots.

SysV Init is fast becoming the standard in the Linux world to control the startup of software at boot time. This is because it is easier to use and more powerful and flexible than the traditional BSD init.

SysV init also differs from BSD init in that the config files are in a subdirectory of `/etc` instead of residing directly in `/etc`. This directory is called `rc.d`. In there you will find `rc.sysinit` and the following directories:

- init.d
- rc0.d
- rc1.d
- rc2.d
- rc3.d
- rc4.d
- rc5.d
- rc6.d

`init.d` contains a bunch of scripts. Basically, you need one script for each service you may need to start at boot time or when entering another runlevel. Services include things like networking, nfs, sendmail, httpd, etc. Services do not include things like setserial that must only be run once and then exited. Things like that should go in rc.local or rc.serial.

If you want rc.local, it should be in /etc/rc.d. Most systems include one even though it doesn't do much. You can also include an rc.serial in /etc/rc.d if you need to do serial port specific things at boot time.

The chain of events is as follows:

- The kernel looks in several places for init and runs the first one it finds
- init runs /etc/rc.d/rc.sysinit
- rc.sysinit does a bunch of necessary things and then runs rc.serial (if it exists)
- init runs all the scripts for the default runlevel.
- init runs rc.local

The default runlevel is decided in /etc/inittab. You should have a line close to the top like:

```
id:3:initdefault:
```

From this, you'd look in the second column and see that the default runlevel is 3, as should be the case for most systems. If you want to change it, you can edit /etc/inittab by hand and change the 3. Be very careful when you are messing with the inittab. If you do mess up, you can fix it by rebooting and doing:

```
LILO boot: linux single
```

This should allow you to boot into single user mode so you can fix inittab.

Now, how does it run all the right scripts? If you enter `ls -l` on `rc3.d`, you might see something like:

```
lrwxrwxrwx 1 root root 17 13:11 S10network -> ../init.d/network
lrwxrwxrwx 1 root root 16 13:11 S30syslog -> ../init.d/syslog
lrwxrwxrwx 1 root root 14 13:32 S40con -> ../init.d/con
lrwxrwxrwx 1 root root 14 13:11 S50net -> ../init.d/net
lrwxrwxrwx 1 root root 13 13:11 S60nfs -> ../init.d/nfs
lrwxrwxrwx 1 root root 15 13:11 S70lpd -> ../init.d/lpd.init
lrwxrwxrwx 1 root root 11 13:11 S91local -> ../rc.local
```

What you’ll notice is that there are no real “files” in the directory. Everything there is a link to one of the scripts in the init.d directory. The links also have an “S” and a number at the beginning. The “S” means to start this particular script and a “K” would mean to stop it. The number is there just for ordering purposes. Init will start all the services based on the order they appear. You can duplicate numbers, but it will only confuse you somewhat. You just need to use a two digit number only, along with an upper case “S” or “K” to start or stop the services you need to.

How does init start and stop services? Simple. Each of the scripts is written to accept an argument which can be “start” and “stop”. You can execute those scripts by hand in fact with a command like:

```
/etc/rc.d/init.d/httpd init stop
```

to stop the httpd server. Init just reads the name and if it has a “K”, it calls the script with the “stop” argument. If it has an “S” it calls the script with a “start” argument. Why all these runlevels? Some people want an easy way to set up machines to be multi-purpose. I could have a “server” runlevel that just runs httpd, sendmail, networking, etc. Then I could have a “user” runlevel that runs xdm, networking, etc.

### 10.5.2 Init Runlevels

Generally, Red Hat Linux runs in run level 3—full multiuser mode. The following runlevels are used in Red Hat Linux:

- 0 Halt.
- 1 Single user mode.
- 2 Multiuser mode, without NFS.

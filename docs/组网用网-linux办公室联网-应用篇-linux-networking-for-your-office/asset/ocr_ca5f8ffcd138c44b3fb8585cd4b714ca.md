directory on the CD-ROM that accompanies this book. Install it as you would any other RPM file, using the rpm command-line utility or gnorpm GUI tool. If you want to find a more recent version of X-ISP, you can check the X-ISP home page at http://users.hol.gr/~dbouras/.

# NOTE

The X-ISP package replaces the /etc/ppp/ip-up and /etc/ppp/ip-down files with enhanced versions of its own. The rpm utility alerts you to this fact, and unless you include the --force flag, it will not permit the installation of X-ISP. If you remove X-ISP and need the original ip-up and ip-down files, you can find them saved under the names ip-up.rpmsave and ip-down.rpmsave, respectively.

By default, X-ISP installs in such a way that only root can use it. If you want other users to be able to dial out, follow these steps:

+   1. Add the users you want to be able to dial out to the group uucp, which should already exist on your system. (These users might need to log out and back on again before these changes will affect them.)
+   2. Change to the /usr/sbin directory and issue the following commands:

```
chown root.uucp chat pppd
chmod 4550 pppd
chmod 550 chat
```

# NOTE

The linuxconf utility tends to reset the permissions on the pppd and chat files, so you might need to perform this operation after you use linuxconf. If you find that this is a problem, you can create a shell script that sets the files' permissions and ownership, and call that script whenever necessary.

In addition to installing and configuring X-ISP, you need to create an /etc/ppp/pap-secrets or /etc/ppp/chap-secrets file, as described in the "PPP Authentication" section earlier in this chapter.

After you've done this, you can start X-ISP by typing xisp at an xterm window, and Linux starts the program, as shown in Figure 8.2.
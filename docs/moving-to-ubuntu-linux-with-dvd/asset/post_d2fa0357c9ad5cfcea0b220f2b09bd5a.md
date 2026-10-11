
If something in that list should prove interesting and you would like to know more about the package, try the `--print-avail` flag. In this example, I try to discover something about the mysterious mtools package:

```
dpkg --print-avail mtools
Package: mtools
Priority: standard
Section: otherosfs
Installed-Size: 468
Maintainer: Luis Bustamante <luberbu@fluidsignal.com>
Architecture: i386
Version: 3.9.9-2.1ubuntu1
Depends: libc6 (>= 2.3.2.ds1-4)
Suggests: floppyy
Size: 195994
Description: Tools for manipulating MSDOS files
```

The preceding information only prints information about an installed package. As with many things in the Linux world (and life in general), there is more than one way to do this. You could also use the other indispensable command-line tool, apt-get—to be specific, apt-cache, one of apt-get’s related utilities:

```
apt-cache show mtools
```

The results of this command are identical to those of the preceding dpkg example.

## Finding out a Package’s Current Release Level

To find out the version of a package that is already installed on your system, use the -l flag. In the following example, I query the system to find out what version of bash (the Bourne Again Shell) I am working with:

```
dpkg -l bash
Desired=Unknown/Install/Remove/Purge/Hold
| Status=Not/Installed/Config-files/Unpacked/Failed-config/
| Half-installed
| Err?=none/Hold/Reinst-required/X=both-problems
(Status,Err: uppercase=bad)
```

```
|| / Name Version Description
++==========================
ii bash 3.1-2ubuntu6 The GNU Bourne Again SHEll
```

## What Is That Strange File?

Let's say that you are wondering what some file is doing on your system. For instance, there is something called pinwrapper in my `/usr/bin` directory and I don't remember installing it. Furthermore, if I try to look it up in the man pages, I am told that there is no information on this file. Using the `-S` flag, I can have `dpkg` identify what package this file was a part of:

```
dpkg -S /usr/bin/pinwrapper
bluez-utils: /usr/bin/pinwrapper
```

Even though I don't remember installing this `bluez-utils` software, I can now use `apt-cache` `show` `bluez-utils` to tell me what this package is for. As it turns out, they are tools for using Bluetooth devices.

## Using apt-get to Install or Update Software

People who use Debian distributions on a regular basis sometimes point to this wonderful little program as the reason why Debian is so great. Well, I certainly won't be the one to deny that `apt-get` is wonderful.

If you want to install a package called `txttype` (a great typing tutor for kids, by the way), this is how to do it:

```
sudo apt-get install txttype
Reading package lists... Done
Building dependency tree... Done
The following extra packages will be installed:
  libssl-image1.2 libssl-mixer1.2
The following NEW packages will be installed
  libssl-image1.2 libssl-mixer1.2 txttype
0 upgraded, 3 newly installed, 0 to remove and 1 not
upgraded.
Need to get 4341kB of archives.
After unpacking 6038kB of additional disk space will be
used.
Do you want to continue [Y/n]?
```

The great thing here is that you do not have to go to a variety of sites to hunt down and identify appropriate software. You call `apt-get` with the `install` parameter and off you go. Notice as well that `apt-get` automatically picks up dependencies for a given package and installs them when needed. If you want to update to the latest version of `txttype`, substitute the `install` parameter with `upgrade`.

I don’t want to confuse things here but speaking of updates, one of the most important things an administrator must do is keep packages up-to-date. You can install upgrades to all installed packages with this version of the `apt-get`:

```
sudo apt-get upgrade
```

Perhaps the most famous example of Debian’s prowess is symbolized by the following command:

```
sudo apt-get dist-upgrade
```

This is, by no means, something that is used on a regular basis. It is used to upgrade from one major release of a distribution to another (say Breezy to Dapper).

## Graphical or Nongraphical?

That is the question, or at least one of them. I routinely work with the command line and with the graphical desktop. Despite my comfort at the command line, I still use Synaptic and find it an invaluable tool.

What should you use? Synaptic is certainly easier for a new user, but the point of showing you these things is two-fold. First, I’d like you to realize that there is more than one way to do it. That applies to graphical tools (as you saw earlier in this chapter) and command-line tools. Second, I want you to see that the shell isn’t that scary, even for dealing with things like software installation. In Chapter 21, the final chapter of this book, I’ll give you a great introduction to working with the Linux shell.

# Chapter 9

# Instant Messaging, and IRC, Too!

Words, words, words... and then a whole lot more words, all of them flowing from one person to another. Whatever cool content exists on the world's Web sites, the Internet is still all about communication.

These days, a new kind of communication has evolved—I call it mini-email. The one-liner. The short and sweet message. The instant message. The Net-connected society has grown to love those quick, always-on means of sending each other information. My own parents (who live in another province) send me a daily one-line weather report via their Jabber instant messaging client. If you are coming from the Windows world, there's a good chance you already have one of these accounts, either with Yahoo!, AOL, MSN, or Jabber.

## Why Jabber?

Because Jabber is an open protocol, it doesn’t belong to anyone in particular, so there is no single company driving its destiny (although there are companies using Jabber). Jabber uses a decentralized approach, so the system is more robust. In fact, anyone can run a Jabber server if he wants to. This is a boon to companies that may want to run a *private, secure* instant messaging network.

> *Trivia Time* Google Talk, an increasingly popular instant messaging service, uses the Jabber protocol.

Whether you choose to run Jabber, Yahoo!, MSN, or something else, the ideal instant messaging client is a multiprotocol client, one that lets you talk to all these services without having to run a client for Jabber, one for AOL, one for Yahoo!, one for . . . well, you get the idea. In this chapter, I’m going to cover two superb Linux instant messaging clients. One is a great multiprotocol client that handles all your favorite chat services. The second is a powerful IRC client.

What’s IRC, you ask? IRC is Internet Relay Chat, and next to your telephone, it is possibly the greatest real-time communication system in the world. I’ll tell you all about it shortly.

## Instant Messaging with Gaim

Gaim is one of the best multiprotocol instant messaging systems out there, period. Furthermore, this is one you can share with the people you know who are still running that other operating system. This is one favor they will thank you for. With Gaim, they no longer need a client for Yahoo!, another for MSN, and yet *another* for AOL because Gaim (gaim.sourceforge.net) is available for Windows as well. It even looks and works the same under both operating systems.

To start Gaim, look under the Applications menu, and then select Internet. You’ll see an entry there for Gaim Internet Messenger. The actual command name is *gaim*, in case you would rather start it from the shell or via the <Alt+F2> run program dialog.

The first time you start up Gaim, you get a simple window with text fields for Account (sometimes known as a *Screen Name*) and Password (see Figure 9-1). The Account field is blank, letting you know that you don't have any accounts set up. Obviously, before we start using instant messaging through Gaim, we are going to need at least one account.

![](img/0e9cf4c65a042f4a9bea644dc50153a7_193_0.png)

**Figure 9-1** First time out with Gaim.

Look below the text fields and you see three buttons labeled Accounts, Preferences, and Sign on. Click the Accounts button and the Accounts window appears (see Figure 9-2). At this stage of the game, there is nothing in it. Click Add, and the Add Account window appears. At the top of that window, you should see a drop-down list labeled Protocol. By default, it says AIM/ICQ. Click the button labeled Protocol and you see a number of possibilities including AIM/ICQ, Gadu-Gadu, GroupWise, IRC, Jabber, MSN, Napster, and Yahoo (see Figure 9-3).

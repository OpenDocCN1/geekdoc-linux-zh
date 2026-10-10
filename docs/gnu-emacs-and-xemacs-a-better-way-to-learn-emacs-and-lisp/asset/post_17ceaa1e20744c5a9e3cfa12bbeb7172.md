
## Chapter 15: External Convenience Packages

- Clipper: A Persistent Clipboard
- Notes Mode
- Folding Mode
- An Interface to Online Dictionaries
- Emacs CD and MP3 Players
- An ABC Mode for Musicians
- The Remembrance Agent

![](img/c8827ea52a0796def3f6891892ed9d3a_294_0.png)

The packages discussed in this chapter were developed by Emacs users who had an itch that needed scratching (in other words, they needed a task that Emacs couldn’t perform). “Scratching” in this context meant writing a new extension for Emacs, a mode or utility that adds yet another costume for this quick-change artist of an editor.

These are external packages, meaning that they aren’t bundled with the official distributions of Emacs (although some might be available as an XEmacs package). Several volumes the size of this one would be required to adequately describe the myriad Emacs extensions that have been written in the past 15 years. Here are my criteria for including packages in this chapter:

- The extension must work with current versions of Emacs and/or XEmacs. Some of the older packages haven’t been updated to work with the recent versions. In many cases, a newer extension with the same functionality has been written.
- It should be freely licensed, preferably under the GNU GPL.
- The add-on should be of use to a reasonably large percentage of readers. Some packages are quite specialized, such as a mode for an obscure programming language that few people use.
- The package shouldn’t have too many bugs and preferably should have an active maintainer.
- It should have enough documentation included. Figuring out how to use the extension shouldn’t be an exercise in interpreting Emacs-Lisp.

All the packages described in this chapter can be found on this book’s CD-ROM in the directory `/cdrom/packages`.

## Clipper: A Persistent Clipboard

You might remember clipper.el from Chapter 7. At the end of that chapter, the Lisp file was lying motionless on the marble slab, its still-quivering organs (pardon me; I meant to say functions!) scattered haphazardly. In the meantime, it has been put back together and sewn up. In this section, you will see what it can do.

Clipper is a fine example of a compact single-file Lisp package (a little over 6 KB). Small as it is, it adds a new mode and an easy-to-use interface to an Emacs session.

Kevin Burton wrote the mode because he was tired of manually copying and pasting the same blocks of text into the comment sections of Lisp files he had written. One of these blocks of text was the obligatory GPL statement found at the beginning of most Emacs–Lisp files. This is how many Emacs extensions are born: Someone faced with repetitious tasks thinks, “Wouldn’t it be nice if Emacs could…”. The idea that Kevin came up with was a permanent file that would act as a repository or memory containing these chunks of text. The hard part was coming up with a way of easily retrieving the units of text by name, plus a quick method of adding new-named text blocks to the repository file. See Chapter 7 if you are interested in the gory details.

## Installation

A single-file package such as Clipper is easy to install. Just copy the file from this book’s CD-ROM into your site-lisp directory, and then insert this Lisp statement into your `~/.emacs` file:

```
(require 'clipper)
```

If you evaluate this line (press Ctr-x Ctrl-c), you will have several new Clipper-related commands to try out:

- M-x clipper-create Creates a new clip.
- M-x clipper-delete Deletes an existing clip.
- M-x clipper-insert Inserts one of your clips into the current buffer.

All three of these commands result in a prompt for a clip’s name. You might also want to set up keybindings for the two commands used most often:

```
(global-set-key [(control c) (control i)] 'clipper-insert)
(global-set-key [(control c) (control n)] 'clipper-create)
```

Although Kevin Burton designed Clipper for inserting “boilerplate” text such as the GNU license, the mode is open-ended enough to be used for any text you repeatedly need to insert, such as your name and mailing address. You could think of Clipper as another form of abbrev-mode (discussed in Chapter 14) but adapted toward larger chunks of text that aren’t needed as often as an abbreviation might be.

## Notes Mode

Notes mode was developed by John Heidemann several years ago as an aid for keeping academic notes organized and accessible. It will probably never be incorporated into the official Emacs distributions, because it isn’t simply an Emacs extension written completely in Lisp. Much of the mode’s functionality derives from several Perl scripts designed to be run periodically and noninteractively in the background. Thus, Notes mode is an unusual hybrid mode, not useful without Emacs as a host (like most modes) but also not useful without a Perl installation and a means of running processes automatically at defined intervals. Luckily, just about every Linux installation fulfills these two requirements: Perl is normally installed by default, and a daemon named cron is available to run programs or scripts periodically.

Notes mode supplies an environment for writing notes and keeping them organized and indexed by date and topic. Like many Emacs extensions, it can be used for purposes not envisioned by the author. Notes mode can be used as a personal database or even as a framework for a journal or diary.

## Prerequisites

You need to have Perl installed, and the version should be at least 5.00. Any recent Emacs or XEmacs version should work. You should have at least several megabytes of disk space available, because the note files and directories inexorably grow in size over time.

## Installation

Notes mode installation is a bit more involved than usual. If it’s done incorrectly, the mode won’t work at all. First, unarchive the distribution file to a temporary directory. Notes mode uses a configure script and makefile system to adapt some of the Lisp files to your system, byte-compile them, and finally copy both the Lisp files and a set of Perl scripts to their new homes.

Running the configure script creates a customized makefile, but the configure process might need to be run with at least one switch, because it might not find your site-lisp directory. The default installation destination for the non-Lisp components is /usr/local, but this can be changed with a switch as well. Here is a sample command:

```
../configure --with-prefix=/usr --with-lisp-dir=/usr/share/emacs/site-lisp --info-dir=/usr/info
```

Use the `--info-dir` switch if you would rather have the Info documentation files somewhere other than the default `/usr/local/info`.

Now load the newly-created makefile into an Emacs session, and look near the top of the file for this section:

```
##################################################
#
# user configurable parameters
#

prefix=/usr

# LIB_DIR should be a private place for notes-mode stuff.
LIB_DIR=$(prefix)/share/notes-mode

# EL_DIR should be where your site-specific emacs .el[.c]s go.
EL_DIR=/usr/share/emacs/site-lisp
# INFO_DIR is for emacs info files.
INFO_DIR=$(prefix)/info
INSTALL_INFO=/usr/sbin/install-info
# must be perl 5.000 or better.
PERL=/usr/bin/perl
# must be 19 or greater
EMACS=emacs
MKDIR_P=mkdir -p
#
       !
# end of user configurable parameters
#
##################################################
```

Check to see if the parameters accurately reflect how you want the package installed. Make any necessary changes and save the file to disk.

XEmacs users need to make one extra edit; change this line:

```
EMACS=emacs
```

to this:

```
EMACS=xemacs
```

This assumes that the XEmacs executable is in your path. Otherwise, type in the path as well—something like this:

```
EMACS=/opt/bin/xemacs
```

Now that the makefile is ready, you can type

```
make install
```

The Lisp files will be byte-compiled in the background by a noninteractive Emacs or XEmacs process and then copied to your site-lisp directory. The Perl scripts are copied to `/usr/local/share/notes-mode` (or else—where if you specified a different prefix), and the Info documentation files join your other Info files. You need to add a line such as the following to the dir file in your Info directory:

```
* Notes Mode: (notes-mode). On-line note organizer
```

There is one last step before you can begin using Notes mode. Change to the directory in which the Perl scripts were installed (the default location is `/usr/local/share/notes-mode`). Execute one of these scripts by typing

```
notesinit
```

This is an interactive script. You will be asked various questions, such as where you want your notes directory to live, and the script uses your answers to complete the setup, creating directories if necessary. Each user on your system must run this script if they want to use the mode.

One task the notesinit script undertakes is setting up your crontab file so that the other Perl utilities are called at the proper intervals. This might or might not work, depending on how cron is configured in your Linux distribution.

Read your cron documentation to find out where the crontab configuration files are located, and check to see if an entry for the Notes mode `mkall` command has been added. If something went wrong and it's not there, you need to add a daily cron job. The following command needs to be executed during the daily cron session:

```
/usr/local/share/notes-mode/mkall
```

For example, on my Debian system, the various cron jobs are in the form of shell scripts located in the directories `/etc/cron.daily`, `/etc/cron.weekly`, and `/etc/cron.monthly`. Here are the contents of a shell script called `notes-mkall`, which runs the `mkall` Perl script once a day:

```
#!/bin/sh
# notes-mode cron daily
/usr/local/share/notes-mode/mkall
```

A script like this needs to be made executable by a command such as this:

```
chmod +x /etc/cron.daily/notes-mkall
```

You really need to make sure that cron is set up to run `mkall` every day, although I suppose you could run the command yourself every day or two. It's nice, though, for your notes index to be kept up-to-date without needing to remember to do it yourself.

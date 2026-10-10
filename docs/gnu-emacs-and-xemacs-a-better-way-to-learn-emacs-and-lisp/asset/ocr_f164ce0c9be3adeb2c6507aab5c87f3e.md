extension written completely in Lisp. Much of the mode’s functionality derives from several Perl scripts designed to be run periodically and noninteractively in the background. Thus, Notes mode is an unusual hybrid mode, not useful without Emacs as a host (like most modes) but also not useful without a Perl installation and a means of running processes automatically at defined intervals. Luckily, just about every Linux installation fulfills these two requirements: Perl is normally installed by default, and a daemon named cron is available to run programs or scripts periodically.

Notes mode supplies an environment for writing notes and keeping them organized and indexed by date and topic. Like many Emacs extensions, it can be used for purposes not envisioned by the author. Notes mode can be used as a personal database or even as a framework for a journal or diary.

# Prerequisites

You need to have Perl installed, and the version should be at least 5.00. Any recent Emacs or XEmacs version should work. You should have at least several megabytes of disk space available, because the note files and directories inexorably grow in size over time.

# Installation

Notes mode installation is a bit more involved than usual. If it’s done incorrectly, the mode won’t work at all. First, unarchive the distribution file to a temporary directory. Notes mode uses a configure script and makefile system to adapt some of the Lisp files to your system, byte-compile them, and finally copy both the Lisp files and a set of Perl scripts to their new homes.

Running the configure script creates a customized makefile, but the configure process might need to be run with at least one switch, because it might not find your site-lisp directory. The default installation destination for the non-Lisp components is /usr/local, but this can be changed with a switch as well. Here is a sample command:

```
```
../configure --with-prefix=/usr --with-lisp-dir=/usr/share/emacs/site-lisp --info-dir=/usr/info
```
```

Use the --info-dir switch if you would rather have the Info documentation files somewhere other than the default /usr/local/info.
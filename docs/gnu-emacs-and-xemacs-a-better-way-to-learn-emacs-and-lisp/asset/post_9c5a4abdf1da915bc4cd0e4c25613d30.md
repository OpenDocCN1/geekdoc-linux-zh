
![](img/c8827ea52a0796def3f6891892ed9d3a_472_0.png)

Figure 72.3 Customizing autosave

  is in a vulnerable state. The phone rings. Your beloved grandmother is in need of assistance, so you jump up from the computer and rush to her aid. Meanwhile, a thunderstorm moves into the area. A nearby lightning strike momentarily interrupts your power, and your computer reboots. What happened to the 280 characters? Did they evaporate into their constituent electrons, as you might expect?

  No, luckily the autosave time-out interval (by default, 30 seconds) elapsed before the lightning strike, and the characters were saved. If you habitually leave your machine without saving your work, you might want to set the interval to 10 or 15 seconds.

  An autosaved file has the same file name as the original file, with the addition of a hash character before and after the name: #filename#. These files are easy to locate in a directory listing or file manager pane when files are listed in alphabetical order (which is usually the case). You will almost always find them at the top of a listing.

  There are two ways to make use of an autosaved file. The first and easiest way is to let Emacs prompt you into renaming the autosaved file to the real file name, overwriting the original file. When Emacs starts up, it takes note of any files that have still-existing autosaved versions. The files that have been autosaved are listed in a hidden subdirectory of your home directory called ~/.emacs.d. Since autosave versions of a file are deleted after you save a buffer, any that are listed in ~/.emacs.d must be the result of a forced Emacs shutdown, such as occurs when power is interrupted or either Emacs or Linux crashes (this is rare, but it can happen).

  When you open a file that has an autosaved version, Emacs asks if you would like to revert the file to the autosaved version. You are shown the relative sizes of the two files. If the autosaved version is larger, consider reverting the file. If you don't revert the file, the next autosave (after you have typed 300 characters) will overwrite the old autosaved file, and then you will have lost what was saved for good.

  If you do decide to use the autosaved file, press M-x and type

`recover-file`

to start the process.

  Emacs prompts you for a file name, giving the current file's name as a default. Normally you can just press Enter, and the deed is done. The `recover-file` command disables autosave for the current file, just in case you want to keep the autosave file as a backup. If the reverted buffer contains your lost material and you proceed to edit the buffer, it is a good idea to re-enable autosave by pressing M-x and typing

`auto-save-mode`

  This might sound complicated, but in practice, you rarely need to think about autosaving. It happens automatically as you work, and you won't even be aware of this protection system until you need it.

## What to Do If You Find a Bug

  You don't need to be a Lisp or C programmer to get involved in Emacs development. If you happen upon a particular editing situation that consistently causes Emacs to misbehave, you might have found a bug in the program. In this situation, you have two options. You can take the passive route, putting up with the bug and hoping someone else has reported it to the developers (most Emacs bugs do eventually get fixed, after all).

  The other option is to make it known that you have found a bug, either by mailing a bug report to a developers' mailing list or by posting a report to the gnu.emacs.bug or gnu.emacs.help newsgroups (see Chapter 23).

  A deramaging or condemnatory attitude will get you nowhere. There is also a possibility that what you interpreted as a bug might be the result of a misunderstanding of some aspect of Emacs' behavior on your part.

  Before you actually report a bug, you should determine whether the problem lies with your particular setup or with an extension package loaded from your `~/.emacs` file. The first thing you should try is this command:

```
emacs -q
```

  If you are running Emacs in a networked environment there may be a site-wide initialization file installed by your system administrator. An additional switch will prevent Emacs from reading that file as well as your personal .emacs file:

```
emacs -q --no-site-file
```

  The `-q` switch causes Emacs to ignore your `~/.emacs` file and start up with the default settings. No packages will be enabled other than the tried-and-true core Lisp files that come with Emacs.

  If you are unable to reproduce your problem with this stripped-down Emacs, your bug is probably with one of the packages. Intuition can help you at this point. Think about the misbehavior and a possible connection with one of your packages. You can load your new-active `~/.emacs` file and activate, one at a time, different packages and try to reproduce the seeming bug. Select the line or lines that enable a particular package, and then select `Evaluate region` from the `Emacs-Lisp` menu.

  If your problem seems to be connected with an extension package, you should contact the maintainer rather than the Emacs developers. Often a question posted on a newsgroup such as `gnu.emacs.help` yields helpful responses by other users of the package.

### Submitting a Bug Report

  Both GNU Emacs and XEmacs have a built-in mode for submitting bug reports via e-mail directly to the maintainers. Try this even if you don't have a bug report as a means of becoming familiar with the process; press `M-x` and type

```
report-emacs-bug
```

  A Mail buffer appears with basic information about your Emacs version and how it was compiled, as shown in Figure 22.4. The logmsg (consisting of the last 100 characters or commands you have typed) is also inserted into the new mail message, which is preaddressed to the appropriate maintainers.

![](img/c8827ea52a0796def3f6891892ed9d3a_475_0.png)

Figure 22.4 A Bug Report Message

  This semi-automated approach to bug reporting not only saves you time, because you don't have to paste the version information and logmsg into the message, but it also helps ensure that the maintainers receive fewer incomplete reports.

  Don't forget to delete the Mail buffer if you aren't actually reporting a bug.

  Both the GNU Emacs and XEmacs Info manuals contain chapters which are a must-read for anyone wanting to report bugs.

## Bug Reporting Tips

  If your report is confirmed by other users and does turn out to be a genuine bug in program code, you might be asked to help track it down. Possibly your version of Linux or the glibc or other shared library differs from those of the developers and/or other users so much so that no one else sees the bug.

  You might be asked to run Emacs with the gdb debugger. If Emacs dumped core, you might be asked to run gdb on the core file. This won't work unless your Emacs binary has been compiled with the -g flag and hasn't been stripped of debugging symbols. You can find out by changing to the directory that holds your Emacs binary and typing:

```
file emacs
```

or

```
file xemacs
```

as the case may be. A message like this means your binary is suitable for use with gdb:

```
emacs: sticky ELF 32-bit LSB executable, Intel 80386, version 1, dynamically linked (uses shared libs), not stripped
```

**If your message looks like this, your binary is unsuitable:**

```
emacs: ELF 32-bit LSB executable, Intel 80386, version 1, dynamically linked (uses shared libs), stripped
```

  If your binary has been stripped, as in the second example, you need to compile a special debugging-enabled Emacs or XEmacs binary.

  This might sound daunting, but it isn't really that difficult to do, assuming that you have a current set of development tools and library headers installed. You should install these packages even if you don't plan to recompile Emacs, because you might need to compile a new Linux kernel at some point.

  If you run the standard GNU Emacs configure script, it generates a makefile that builds a debugging-enabled Emacs binary. The configure script supplied with the source for stable versions of XEmacs is not set up for debugging. You need to run the configure script with debugging explicitly enabled:

```
./configure --debug
```

  As soon as you are running a debugging-enabled Emacs, you can run Emacs under the control of the GNU debugger, gdb, with this command:

```
gdb emacs
```

  The Gdb Info manual gives you the information you need to be able to induce gdb to generate messages and reports that will be useful to developers. For brief usage information, you can type

```
gdb --help
```

  If you ask the developer to whom you reported the bug for assistance, you might receive help in the form of a command or procedure you can follow. You can find a

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

# ## Submitting a Bug Report

Both GNU Emacs and XEmacs have a built-in mode for submitting bug reports via e-mail directly to the maintainers. Try this even if you don't have a bug report as a means of becoming familiar with the process; press `M-x` and type

```
report-emacs-bug
```

A Mail buffer appears with basic information about your Emacs version and how it was compiled, as shown in Figure 22.4. The logmsg (consisting of the last 100 characters or commands you have typed) is also inserted into the new mail message, which is preaddressed to the appropriate maintainers.
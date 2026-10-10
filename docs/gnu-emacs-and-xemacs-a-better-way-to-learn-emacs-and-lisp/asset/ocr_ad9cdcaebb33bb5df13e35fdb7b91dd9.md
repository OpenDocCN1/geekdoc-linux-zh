If you are unsure, try typing `emacs` or `xemacs` in an xterm window, and see if anything happens! If an Emacs window appears, press M-x and then type this command in the minibuffer:

```
emacs-version
```

The version of Emacs you are running is displayed. Compare the version number with the version numbers of the packages on the CD-ROM. If yours is older, consider removing your installed version and replacing it with the appropriate package from the CD-ROM.

# The Emacs Maintainer’s Role

Part of the job of putting together a Linux distribution is picking the right people to maintain the various packages. In free-software lingo, to maintain a package is to be responsible for keeping up with changes in the upstream source, which is the source code from the developer(s) of the software the package is based on. The maintainer also forwards bug reports to the upstream developers and possibly even fixes bugs and contributes enhancements.

For many Linux users, Emacs is an important application. A well-run distribution carefully chooses its official Emacs maintainer, ideally a skilled Emacs user who keeps up with changes in Emacs.

Here are some of the tasks an Emacs package maintainer is expected to do:

+   - After the Emacs makefile so that the editor is installed in the correct directory for the particular distribution.
+   - Keep up with user bug reports and other mail.
+   - Incorporate distribution documentation and other files into the package.
+   - Coordinate efforts with the main distribution release team.
+   - Forward bug reports and fixes to the upstream Emacs maintainers.
+   - Apply needed patches to the current Emacs source release that might have surfaced since the last official Emacs release. These may come from users or developer mailing lists.

# Red Hat Emacs

The Red Hat packages on the CD-ROM correspond with Red Hat 7.1, the most current release when this book was published. Both GNU Emacs and XEmacs packages can be found in the directory /binary/dists/redhat.
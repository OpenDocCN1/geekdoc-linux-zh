Although dselect supports a few command-line options, they're mostly obscure or minor (such as options to set the color scheme). Consult dselect's man page for details. To use the program, type dselect. The result is the dselect main menu, as shown running in a KDE Konsole window in Figure 2.1.

# FIGURE 2.1 The dselect utility provides access to APT features using a menu system.

![](bbox=[0.22, 0.24, 0.76, 0.52])

Another text-based Debian package manager is aptitude. In interactive mode, aptitude is similar to dselect in a rough way, but aptitude adds menus accessed by pressing Ctrl+F and rearranges some features. You can also pass various commands to aptitude on the command line, as in aptitude search samba, which searches for packages related to Samba. Features accessible from the command line (or the interactive interface) include the following:

+   * **Update package lists** You can update package lists from the APT repositories by typing aptitude update.
+   * **Install software** The install command-line option installs a named package. This command has several variant names and syntaxes that modify its action. For instance, typing aptitude install zsh installs the zsh package, but typing aptitude install zsh- and aptitude remove zsh both uninstall zsh.
+   * **Upgrade software** The full-upgrade and safe-upgrade options both upgrade all installed packages. The safe-upgrade option is conservative about removing packages or installing new ones and so may fail; full-upgrade is less conservative about these actions and so is more likely to complete its tasks, but it may break software in the process.
+   * **Search for packages** The search option, noted earlier, searches the database for packages matching the specified name. The result is a list of packages, one per line, with summary codes for each package's install status, its name, and a brief description.
# Chapter 2 • Managing Software

Although dselect provides few command-line options, they're mostly obscure or minor (such as options to select the color scheme). Consult dselect's man page for details. To use the program, **dselect**. The result is the dselect main menu, as shown running in a KDE Console window in Figure 2.1.

# FIGURE 2.1 The dselect utility provides to APT features using a menu

![](bbox=[0.218, 0.233, 0.761, 0.526])

Another text-based Debian package manager is aptitude. In interactive mode, aptitude is similar to dselect in a rough way, but aptitude adds menus accessed by pressing Ctrl+T and rearrangements around features. You can also pass various commands to aptitude on the command line, in aptitude samba, which searches for packages related to Samba. Features accessible from the command line (or the interactive interface) include the following:

**Update Package Lists** You can update package lists from the APT repositories by typing **aptitude update**.

**Install Software** The install command-line option installs a named package. This command has several name and syntaxes that modify its action. For instance, typing **aptitude install zsh** installs the package, by typing **aptitude install zsh-** (with a trailing dash) and **aptitude remove zsh** both uninstall zsh.

Upgrade Software The full-upgrade and safe-upgrade options upgrade all installed packages. The safe-upgrade option is conservative about removing packages or installing new ones and so may fail; full-upgrade is less conservative about these actions and so is more likely to complete its tasks, but it may break software in the process.
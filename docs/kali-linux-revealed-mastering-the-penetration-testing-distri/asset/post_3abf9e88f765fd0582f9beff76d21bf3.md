
![](img/46e3313ea1bb2892f314630a4f0677b8_217_0.png)

When you run aptitude, you are shown a list of packages sorted by state (installed, not-installed, or installed but not available on the mirrors), while other sections display tasks, virtual packages, and new packages that appeared recently on mirrors. To facilitate thematic browsing, other views are available.

In all cases, aptitude displays a list combining categories and packages on the screen. Categories are organized through a tree structure, whose branches can respectively be unfolded or folded with the Enter, [, and ] keys. The + key should be used to mark a package for installation, - to mark it for removal, and ~ p to purge it. Note that these keys can also be used for categories, in which case the corresponding actions will be applied to all the packages of the category. The u key updates the lists of available packages and Shift+u prepares a global system upgrade. The g key switches to a summary view of the requested changes (and typing g again will apply the changes), and q quits the current view. If you are in the initial view, this will close aptitude.

## aptitude's Documentation

This section does not cover the finer details of using aptitude, it rather focuses on giving you a user survival kit. aptitude is rather well documented and we advise you to use its complete manual available in the *aptitude-doc-en* package.

```
⇒ file:///usr/share/doc/aptitude/html/en/index.html
```

To search for a package, you can type / followed by a search pattern. This pattern matches the name of the package but can also be applied to the description (if preceded by ~d), to the section (with `-s`), or to other characteristics detailed in the documentation. The same patterns can filter the list of displayed packages: type the l key (as in limit) and enter the pattern.

Managing the automatic flag of Debian packages (see section 8.3.4, “Tracking Automatically Installed Packages” [page 199]) is a breeze with aptitude. It is possible to browse the list of installed packages and mark packages as automatic with Shift-m or you can remove the mark with the m key. Automatic packages are displayed with an “A” in the list of packages. This feature also offers a simple way to visualize the packages in use on a machine, without all the libraries and dependencies that you don't really care about. The related pattern that can be used with l (to activate the filter mode) is -il-M. It specifies that you only want to see installed packages (-i) not marked as automatic (t-M).

### Using aptitude on the Command-Line Interface

Most of Aptitude's features are accessible via the interactive interface as well as via the command-line. These command-lines will seem familiar to regular users of apt-get and apt-cache. The advanced features of aptitude are also available on the command-line. You can use the same package search patterns as in the interactive version. For example, if you want to clean up the list of manually installed packages, and if you know that none of the locally installed programs require any particular libraries or Perl modules, you can mark the corresponding packages as automatic with a single command:

```
# aptitude markauto `~slibs|~sperl`
```

Here, you can clearly see the power of the search pattern system of aptitude, which enables the instant selection of all the packages in the libs and perl sections. Beware, if some packages are marked as automatic and if no other package depends on them, they will be removed immediately (after a confirmation request).

### Managing Recommendations, Suggestions, and Tasks

Another interesting feature of aptitude is the fact that it respects recommendations between packages while still giving users the choice not to install them on a case-by-case basis. For example, the gnome package recommends gdebi (among others). When you select the former for installation, the latter will also be selected (and marked as automatic if not already installed on the system). Typing g will make it obvious: gdebi appears on the summary screen of pending actions in the list of packages installed automatically to satisfy dependencies. However, you can decide not to install it by deselecting it before confirming the operations.

Note that this recommendation tracking feature does not apply to upgrades. For instance, if a new version of gnome recommends a package that it did not recommend formerly, the package won't be marked for installation. However, it will be listed on the upgrade screen so that the administrator can still select it for installation.

Suggestions between packages are also taken into account, but in a manner adapted to their specific status. For example, since gnome suggests dia-gnome, the latter will be displayed on the summary screen of pending actions (in the section of packages suggested by other packages). This way, it is visible and the administrator can decide whether to take the suggestion into account or not. Since it is only a suggestion and not a dependency or a recommendation, the package will not be selected automatically—its selection requires manual intervention (thus, the package will not be marked as automatic).

In the same spirit, remember that **aptitude** makes intelligent use of the concept of tasks. Since tasks are displayed as categories in the screens of package lists, you can either select a full task for installation or removal or browse the list of packages included in the task to select a smaller subset.

## Better Solver Algorithms

To conclude this section, let's note that **aptitude** has more elaborate algorithms compared to **apt** when it comes to resolving difficult situations. When a set of actions is requested and when these combined actions would lead to an incoherent system, **aptitude** evaluates several possible scenarios and presents them in order of decreasing relevance. However, these algorithms are not foolproof. Fortunately, there is always the possibility to manually select the actions to perform. When the currently selected actions lead to contradictions, the upper part of the screen indicates a number of broken packages (you can directly navigate to those packages by pressing b). Then you can manually build a solution. In particular, you can get access to the different available versions by selecting the package with Enter. If the selection of one of these versions solves the problem, you should not hesitate to use the function. When the number of broken packages gets down to zero, you can safely go to the summary screen of pending actions for a last check before you apply them.

### Aptitude's Log

Like **dpkg**, **aptitude** keeps a trace of executed actions in its logfile (`/var/log/aptitude`). However, since both commands work at a very different level, you cannot find the same information in their respective logfiles. While **dpkg** logs all the operations executed on individual packages step by step, **aptitude** gives a broader view of high-level operations like a system-wide upgrade.

Beware, this logfile only contains a summary of operations performed by **aptitude**. If other front-ends (or even **dpkg** itself) are occasionally used, then **aptitude**'s log will only contain a partial view of the operations, so you can't rely on it to build a trustworthy history of the system.

## Synaptic

Synaptic is a graphical package manager that features a clean and efficient graphical interface (shown in Figure 8.2, “synaptic Package Manager” [page 194]) based on GTK+ and GNOME. Its many ready-to-use filters give fast access to newly available packages, installed packages, upgradable packages, obsolete packages, and so on. If you browse through these lists, you can select the operations to be done on the packages (install, upgrade, remove, purge); these operations are not performed immediately, but put into a task list. A single click on a button then validates the operations and they are performed in one go.

![](img/46e3313ea1bb2892f314630a4f0677b8_220_0.png)

# 8.3. Advanced APT Configuration and Usage

Now it is time to dive into some more advanced topics. First, we will take a look at advanced configuration of APT, which will allow you to set more permanent options that will apply to APT tools. We will then show how package priorities can be manipulated, which opens the door for advanced fine-tuned, customized updates and upgrades. We will also show how to handle multiple distributions so that you can start experimenting with packages coming from other distributions. Next, we will take a look at how to track automatically installed packages, a capability that enables you to manage packages that are installed through dependencies. We will also explain how multi-arch support opens the door for running packages built for various hardware architectures. Last

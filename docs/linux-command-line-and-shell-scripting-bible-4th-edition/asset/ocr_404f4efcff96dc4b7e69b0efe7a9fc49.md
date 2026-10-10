configuration. Thus, you might press the Alt+U key combination to undo the last task within nano.

Even more features are available through command-line options to control the nano editor. Creating a backup file before editing is one nice selection. Type man nano to see these additional command-line options for starting nano.

The vim and nano text editors offer a choice between powerful and simple console mode text editors. However, neither offers the ability to use graphical features for editing. Some text editors can operate in both worlds, as explored in the next section.

# Exploring the Emacs Editor

The Emacs editor was an extremely popular editor for Digital Equipment Corporation (DEC) computers in the late 1970s.
Developers liked it so much that they ported it to the Unix environment, and then to the Linux environment, where its official name is GNU Emacs. Though currently not as popular as vim, it still has its place in the world.

The Emacs editor started out life as a console editor, much like vim, but was migrated to the graphical world. The original console mode editor is still available, but it can use a graphical window to allow editing text in a graphical environment. Typically, when you start the Emacs editor from a command line, if the editor determines you have an available graphical session, it starts in graphical mode. If you don't, it starts in console mode.

This section describes both the console mode and graphical mode Emacs editors so that you'll know how to use either one if you want (or need) to.

# Checking your Emacs package

Many distributions do not come with the Emacs editor installed by default. You can check your Red Hat–based distribution by using the which and/or dnf list (use yum list on older versions of Red Hat-
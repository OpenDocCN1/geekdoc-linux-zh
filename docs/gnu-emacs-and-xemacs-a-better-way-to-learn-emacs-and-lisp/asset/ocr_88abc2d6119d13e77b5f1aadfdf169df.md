Just beneath the Merge submenu is the Apply Patch submenu. You can choose to patch either a single file or an entire directory. The latter option is more commonly used. Most patches include sections of differences, each of which is intended for a different file in a directory of source code.

If you are patching a directory, an Ediff session group is displayed, with each file affected by the patch becoming a session. This allows you to patch each file indi-vitually if you wish. The buffer is similar to Figure 14.9.

# Learning More

Ediff comes with an informative Info manual that contains more details than this book can give. A good way to become comfortable and gain facility with Ediff is to try it out on unimportant files. It takes a while to get used to the dual-keyboard mode (commands working only while the control window has the focus), but a little practice will help.

If you use Ediff often, consider taking a look at the variables that can be changed with Customize. The Ediff Customize group is quite large and contains dozens of changeable settings, including the highlighting faces used on difference regions.

# Spell Checking with ispell

Most, if not all, word processors offer some form of spell checking, a service that can be a time-saver for those who can't spell well. Typically, the dictionary database used by the application isn't used by other programs. This can lead to multiple bulky dictionaries, each used by a different piece of software. The philosophy be-hind UNIX and UNIX-like systems like Linux includes the idea of small but powerful tools that cooperate with each other. One dictionary available for all pro-grams is a natural outgrowth of this view.

Emacs doesn't come with a dictionary, yet checking the spelling for entire docu-ments, a selected region, or a single word is just a keystroke away. This is possible because Emacs makes use of the default system-wide dictionary system present on nearly all computers running Linux, ispell.

ispell has been around in one form or another since 1971, when an ancestral ver-sion was written for the WAITS operating system on DEC PDP-10 computers. The current maintainer is Geoff Knueling. It is an international program with dictionaries available for many languages.

ispell is a stand-alone command-line program that is used like this:
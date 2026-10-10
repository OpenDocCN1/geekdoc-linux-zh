should work with any version of Emacs after you've added the new Info directory as just described. A utility called install-info is a part of most Linux distributions. This program can be a Perl script or a compiled C program, depending on the distribution. All the versions make it easy for software authors to install associated Info files and add the appropriate index entry to the dir file. You can also use the utility yourself if you need to install an Info file manually, but it might be easier to just add the entry yourself rather than figure out the proper switches for an install-info command.

This isn't hard to do as long as you follow a few formatting rules needed for a valid entry. Here is an example:

+   * Ispell: (ispell) ISPELL, an interactive spelling corrector.

The field on the right is a brief description that isn't absolutely necessary. The field on the left must follow this sequence:

+   * An asterisk followed by one space
+   * The English name of the program, followed by a colon and a space
+   * The actual name of the Info file (stripped of the .info suffix)
+   * Parentheses must surround the actual name
+   * A period follows the right parenthesis
+   * At least one space or tab separates the left and right fields

After adding an entry, you can check it by starting up Info in an Emacs session. If the new link entry is valid, it is highlighted like the other entries. Clicking the new entry should load the new manual.

Emacs constructs its composite dir file the first time you start up the Info reader. If you make changes to one of the dir files (such as adding a new entry), you need to exit Emacs and restart it so that your change will be recognized.

# Finding Help on the Net

Few events have benefited the free software community more than the advent of common and inexpensive Internet access. The constant flow of patches, ideas, and requests for help is an asset to both users and developers. The Internet has grown to such an extent in recent years that it can be difficult to find the particular online community that has the information you need. This section offers pointers to the areas of the Net that offer the most help and information to the Emacs user.
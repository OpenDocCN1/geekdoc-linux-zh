warn you about the one-in-a-thousand situation, rather because you should worry. In practice, I’ve found that Microsoft Office–formatted files are more compatible with OpenOffice.org than they are with other versions of Microsoft Office!

If you are going to be using the revision-tracking feature of OpenOffice.org (found under Edit | Changes), you might want to set some preferences under the OpenOffice.org node, User Data subnode. If you don’t at least enter your name and initials, your changes will appear to other users to have been made by Unknown User, which may or may not be what you intended.

Also under the OpenOffice.org node is the Paths subnode. In this screen you can define where OOO looks for files. You may want to tweak some of these paths depending on your particular needs. I already discussed the default save path—the My Documents type. If you use your own document templates, you may not want to store them in the default location of `/usr/lib/openoffice/share/template/english`. I don’t, because it’s a bad idea to keep your own data buried in the bowels of program directories. I keep all my own templates in a directory on the file server where everyone can access them, and where I can easily back them up.

There are already some templates in the default directory, supplied by the OOO installation. You don’t necessarily want to lose access to those; conveniently, you can add your own template path to the existing path. Select the Templates type from the list, click Edit to display the Select Paths dialog, and then click Add. Use the file drill-down box to select the folder you want to add to the path. See Figure 9.

![](bbox=[0.08, 0.5, 0.97, 0.93])

**Figure 9.** You can add your own template directory to the template path.
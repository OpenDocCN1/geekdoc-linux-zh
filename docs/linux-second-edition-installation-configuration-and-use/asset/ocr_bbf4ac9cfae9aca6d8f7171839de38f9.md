+   Your LaTeX text begins with the instruction \documentstyle[options]{{type} (instead of \documentclass). As options, you specify not only the options described on page 598, but also the names of additional files which in LaTeX are loaded with \usepackage. An analogous command to \usepackage does not exist in LaTeX 2.09.

+   For changing character sets, the only available commands are \m, \fs, \tt, \bf, \it, \sc and \em. Combination of type attributes is only possible to a very limited extent. The commands for changing the type size \small, \large automatically activate the standard font – if you want to change the type size for \tt, you must first specify the command and then \tt (and not vice versa).

+   The Tb environment mentioned in the previous section does not exist. Therefore, you cannot use the macro described above for the new sybox environment. So affected.

It is quite possible to live with these restrictions. The real functionality of LaTeX (setting of formulae, scientific layout elements, and so on) is not

# Compatibility problems with LaTeX2

Totally different problems can occur when you try to produce a text generated previously with LaTeX 2.09 with the new LaTeX 2e automatically activates a compatibility mode when a document begins with \documentclass instead of \documentclass. In this case, it tries to behave exactly in the same way as LaTeX 2.09. In principle, this compatibility mode works very well. The fact that problems will arise, in spite of this, has mainly two causes:

+   The text uses macro files which are no longer available under LaTeX 2e or have a different name. This problem can be easily overcome by copying the file in (usually name.sty) from your old LaTeX version into your current working directory. If you have already deleted LaTeX 2.09 on your computer (for example, during installation of a new LINUX distribution), you must try to obtain the file from another computer (if necessary, via the Internet).

+   The text uses macro files in which additional character sets or type style commands are defined. These files are usually predecessor versions of the new type style commands of LaTeX 2e, which could already be used in LaTeX 2.09. In these predecessor versions, however, some different file names and a different syntax apply. Your best chance of processing such tasks is to try to convert the files to LaTeX 2e. In many cases you will just have to modify the file header (that is, \documentclass and \usepackage instead of the old \documentclass). You might also have to search for and replace some type style commands with their new counterparts
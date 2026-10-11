# Creating archives

Run File Roller by clicking Main Menu | Accessories | File Roller (see Figure 1).

![](bbox=[0.08, 0.13, 0.85, 0.36])

*Figure 1. The main File Roller screen before adding files to an archive.*

To create an archive, the first thing you do is create an archive. Ho, ho, ho. Just love saying that. With WinZip, you can create archives on the fly after selecting a bunch of files, or by creating an archive file, sort of as an empty shell. With File Roller, you don't have both options; you need to create the archive file first. Then you add files to it.

To create an archive file, first click the New button on the toolbar (select Archive | New from the menu, or press Ctrl-N) to open the New Archive dialog. Enter a name for the archive file, and then select the type of archive by opening the Archive Type combo box, shown in *Figure 2*.

If you enter an extension with the name of the archive, keep Archive Type set to “Automatic,” and File Roller will automatically determine the archive type from the extension you're using. If you choose an archive type, don't include an extension with the file name, and the appropriate extension will be added to the archive once it's created. In either case, click OK to return to the main File Roller dialog, as shown in *Figure 3*.

You can see the name of the archive in the title bar. In *Figure 3*, the archive is named “SampleArchive.tar.gz”. If you decide to abandon the archive process before adding files to the archive file, File Roller will delete the newly created archive file.

Now that you've got an archive file started, add files to it. Click the Add button in the toolbar (or use the menu, or a keystroke combination) to open the Add Files dialog, shown in *Figure 4*. You can also drag files from Nautilus into File Roller.

In *Figure 4*, I've highlighted three of four files in the directory /home/whill/RollerStuff.

In *Figure 4*, I've highlighted three of four files in the directory /home/whill/RollerStuff. Clicking the OK button will add those files to the archive, resulting in a main File Roller dialog, shown in *Figure 5*.

Note that in *Figure 2* you could have selected a simple archive, without compression, such as the “tar uncompressed (.tar)” option. Doing so would have resulted in a file named SampleArchive.tar.

Once you've added files to an archive, the disabled options in *Figure 4* become available. You can choose from a variety of advanced options. For example, you've choose just certain files, according to file name masks (such as *.txt to add just files with a .txt extension) that you enter in the Selection text box. Another option is to add files only if there isn't a newer version already in the archive.
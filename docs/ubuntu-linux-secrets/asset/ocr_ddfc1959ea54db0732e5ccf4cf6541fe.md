# Filenames

In the old days of Windows (such as in the popular versions 3.0 and 3.1), there were strict limitations on what you could name your files. The standard in Windows was called the 8.3 format. This format prescribed

+   ♦ An eight-character name that couldn't use spaces or many special characters
+   ♦ A period
+   ♦ A three-character file extension, usually consisting of letters

In Windows the file extension determined the type of file the filename referred to. Application files that could be run on the system had to have file extensions of .exe or .com. Text script files used a file extension of .bat. Data files for individual applications also had their own file extension. If you used the Microsoft Office productivity software suite, Word documents ended in .doc, Excel documents ended in .xls, and PowerPoint documents ended in .ppt.

Newer versions of Windows did away with the 8.3 file naming format. You can now use any length of filename and almost about any characters you wish. However, Windows did retain the three-character file extension as part of the filename. The extension still indicates the type of file so that Windows knows how to handle it.

Ubuntu (and Linux in general) doesn't require file extensions on files per se, but it does utilize them. Executable files in Ubuntu are marked by a permissions setting on the file (see Chapter 17, "Users and Groups"). They don't require any special file extension on the filename.

There is one special category of files in Ubuntu that's important to know. Files that begin with a period are called hidden files. Hidden files are configuration files used for various applications, as well as the Linux operating system itself. They're called hidden because the default way of handling the files, whether using graphical or command line tools, is to ignore files that begin with a period. To view hidden files you need to set your file management program to display them (see Chapter 19, "The Ubuntu Command Line").

In the Windows world you're used to using graphical tools to manage files and folders. Ubuntu also contains a graphical tool, called Nautilus, that you can use to manage your files and folders. The next section describes the Nautilus tool and how to use it.

# Nautilus

The Nautilus application is a GNOME utility that provides access to files and folders using a graphical interface. Ubuntu uses Nautilus for all desktop file management functions. To get the most out of your Ubuntu desktop, you'll need to know how to use Nautilus. The following sections describe Nautilus and how to perform most common file management features with it.

# Nautilus Window Components

The default Nautilus mode used by Ubuntu is Browser mode. In Browser mode, Nautilus operates much like a web browser. Figure 5-2 shows viewing a folder in Browser mode.
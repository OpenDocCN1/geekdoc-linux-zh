# mkisofs

To create a CD image, you first select the files you want on your CD. Then you can use mkisofs to create an ISO CD image of them.

# mkisofs Options

You may need to include several important options with mkisofs to create a data CD properly. The -o option is used to specify the name of the CD image file. This can be any name you want to give it. The -R option specifies RockRidge CD protocols, and the -J option provides for long Windows 95/98/ME or XP names. The -r option, in addition to the RockRidge protocols (-R), sets standard global permissions for your files, such as read access for all users and no write access because the CD-ROM is read-only. The -T option creates translation tables for filenames for use on systems that are not RockRidge-compliant.

The -U option provides for relaxed filenames that are not standard ISO-compliant, such as long filenames, those with more than one period in their name, those that begin with a period such as shell configuration files, and ones that use lowercase characters (there are also separate options for each of these features if you just want to use a few of them). Most RPM and source code package names fall in this category. The -iso-level option lets you remove ISO restrictions such as the length of a filename. The -V option sets the volume label (name) for the CD. Finally, the -v option displays the progress of the image creation.

# Disk Image Creation

The last argument is the directory that contains the files for which you want to make the CD image. For this, you can specify a directory. For example, if you are creating a CD-ROM to contain the data files in the mydocs directory, you would specify that directory. This top directory will not be included, just the files and subdirectories in it. You can also change to that directory and then use . to indicate the current directory.

If you were creating a simple CD to use on Linux, you would use mkisofs to first create the CD image. Here the verbose option will show the creation progress, and the -V option lets you specify the CD label. A CD image called songs.iso is created using the file located in the newsong directory:

```
mkisofs -v -V "Goodsongs" -o moresongs.iso newsongs
```

If you also wanted to use the CD on a Windows system, you would add the -r (RockRidge with standard global file access) and -J (Joliet) options:

```
mkisofs -v -r -J -V "Goodsongs" -o moresongs.iso newsongs
```

You need to include certain options if you are using filenames that are not ISO compliant, such as ones with more than 31 characters or ones that use lowercase characters. The -U option lets you use completely unrestricted filenames, whereas certain options like -L for the unrestricted length will release specific restrictions only. The following example creates a CD image called mydoc.iso using the files and subdirectories located in the mdoc directory and labels the CD image with the name "doc":

```
mkisofs -v -r -T -J -U -V "Greatdocs" -o mydocuments.iso mydocs
```
# Chapter 6: Installing Your Web Server Software

options in the access.conf file or define directories for scripts by adding lines to the httpd.conf file.

The access and other options are set to "safe" values for most uses by default. If you install your OpenLinux system while you have a live Internet connection and your machine is visible on the Internet, anyone can immediately use the Web server on your OpenLinux system. But the configuration is such that you shouldn't worry about security.

In addition to the three files just mentioned, another file in the conf/ directory is mime.types. MIME refers to Multipurpose Internet Mail Extensions, a system of defining the type of a file so that it can be acted upon by the appropriate application. This is something like associating a file with the .GIF extension to open in a graphics viewer. The mime.types file defines all the data types that the Web server recognizes, with an associated file extension.

For example, the default mime.types file includes the following line:

```
video/quicktime                qt mov
```

If you include a link to a file with the extension .qt or .mov, the Web server can indicate to the requesting browser in its header information that the file is of video/quicktime. If the browser has data type included in its configuration file, it will know what application to start that file when it is downloaded.

The mime.types file on the Web server is just a service to browsers. Each browser may also have a similar configuration file and ignore the information provided by the Web server with the incoming file. Still, you should keep the mime.types file up to date when you become aware of other data types that you are delivering as part of your pages.

# Using a Text Editor

As you review configuration files, you can use any number of text editors to edit the files to fit your needs. The standard OpenLinux Lite installation includes a popular UNIX editor you might be familiar with: vi. Other standard editors like emacs and joe are included on the CD-ROM. Use the rpm command to install the one you prefer.

You can start the vi editor in character mode or any terminal window with the following command:

```
vi filename
```

Alternatively, if you work in a graphical environment, you can start the CRISLite editor from the icon on the OpenLinux desktop. This menu-based editor, shown in Figure 6-1 with the Apache configuration files, makes it a lot easier to get started editing files in Linux. Just use the File | Open menu to locate the configuration files you need to edit.
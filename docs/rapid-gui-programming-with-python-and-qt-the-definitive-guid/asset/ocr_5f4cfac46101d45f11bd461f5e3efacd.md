line from a different directory—for example, ,/chap06/imagechanger .pyw—none of the icons will appear. This is because we gave the icon's path as ,images, that is, a path relative to the application's working directory, so when invoked from elsewhere, the icons were looked for in the .,images directory (which might not even exist), when in fact they are in the .,/chap06/images directory.

We might be tempted to try to solve the problem using Python's os.getcwd() function; but this returns the directory where we invoked the application, which as we have noted, may not be the directory where the application actually resides. Nor does PyQt's Qappliation.applicationDirPath() method help, since this returns the path to the Python executable, not to our application itself. One solution is to use os.path.dirname(_ _file _ _) to provide a prefix for the icon filenames, since the _ _file_ variable holds the full name and path of the current . py or .pyw file.

Another solution is to put all our icons (and help files, and any other small resources) into a single .py module and access them all from there. This not only solves the path problem (because Python knows how to look for a module to be imported), but also means that instead of having dozens of icons, help files, and similar, some of which could easily become lost, we have a single module containing them all.

To produce a resource module we must do two things. First, we must create a .qrc file that contains details of the resources we want included, and then we must run pyrcc4 which reads a .qrc file and produces a resource module. The .qrc file is in a simple XML format that is easy to write by hand. Here is an extract from the resources .qrc file used by the Image Changer application:

```
"""
```
<RCC version="1.0">
  <qresource>
    <file alias="filenew.png">images/filenew.png</file>
    <file alias="fileopen.png">images/fileopen.png</file>
    ...
    <file alias="icon.png">images/icon.png</file>
    <file>help/editmenu.html</file>
    <file>help/filemenu.html</file>
    <file>help/index.html</file>
  </qresource>
</RCC>
```"""
```

The ellipsis represents many lines that have been omitted to save space because they are all very similar. Each file entry must contain a filename, with its relative path if it is in a subdirectory. Now, if we want to use the "file new" action's image, we could write QIcon(". /images/filenew.png"). But thanks to the alias, we can shorten this to QIcon("filenew.png"). The leading :/ tells PyQt that the file is a resource. Resource files can be treated just like normal (read-only) files in the filesystem, the only difference being that they have the
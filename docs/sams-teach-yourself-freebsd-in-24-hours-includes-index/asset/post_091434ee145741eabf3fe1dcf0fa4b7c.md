
> If the idea of customizing software seems scary to you, don't worry. You don't need to know anything about programming in order to do this. All you have to do is tell the installer what options you want to build the source code with, and it will worry about how to actually include those options in the finished product. You will see how to do this later in this hour.

## Discovering What's Available

The easiest way to find out what kind of software is available for FreeBSD is to browse around the ports page on the FreeBSD Web site. It is located at the address www.freebsd.org/ports.

Figure 6.1 shows the main ports page on the FreeBSD Web site.

FIGURE 6.1
A section of the main ports page on the FreeBSD Web site. Notice that the software is categorized according to its intended purpose.

![](img/ba0161b65b37e94cffc801ecbacaba5e_115_0.png)

Clicking on any one of the categories will take you to a list of software available in that category. For example, Figure 6.2 shows a section of the Graphics category.

FIGURE 6.2
A section of the Graphics category on the ports page showing some of the graphics-related applications available for FreeBSD.

![](img/ba0161b65b37e94cffc801ecbacaba5e_116_0.png)

When you've found an application that interests you, simply remember what category it was under and then you can proceed with installing it. Previously, we mentioned that two methods are available for installing FreeBSD applications. We will look at both of them, starting with the prebuilt package method. For our examples, we will assume that you are interested in the GIMP software. GIMP is a freely available image editing program that has features similar to Adobe Photoshop.

## Installing Software from Prebuilt Packages

Prebuilt packages can be downloaded from the FreeBSD FTP server or one of its mirrors. If you've never worked with FTP before, the easiest way for you to do it will be from a Web browser. If you are working from the FreeBSD command line, you can use the Lynx Web browser, which is text based, but will work fine for our purposes here. To start the Lynx Web browser and point it to the main FreeBSD FTP server's package directory, enter the following command:

```
lynx ftp://ftp.freebsd.org/pub/FreeBSD/ports/packages
```

Note that it is case sensitive, so the command must be typed exactly as shown; otherwise you will get an error.

After the connection has been made, you should see a screen that looks like Figure 6.3.

FIGURE 6.3
The Lynx Web browser connected to the FreeBSD package FTP server.

![](img/ba0161b65b37e94cffc801ecbacaba5e_117_0.png)

Use the arrow keys to navigate down the list until the graphics directory is highlighted and then press the Enter key. After the screen has reloaded, it should look similar to Figure 6.4.

FIGURE 6.4
Inside the graphics directory. The files ending in .tgz are the package files.

![](img/ba0161b65b37e94cffc801ecbacaba5e_117_1.png)

Once again, simply use the arrow keys to scroll down the list until you have found the GIMP package.

You can use the space bar to scroll forward in the list by an entire page.

The list of packages is in a semi-alphabetical format. All package names beginning with numbers are listed first. After this, all packages beginning with uppercase letters are listed in alphabetical order. This is followed by all packages beginning with lowercase letters listed in alphabetical order.

Figure 6.5 shows the screen with the GIMP package highlighted.

FIGURE 6.5
The GIMP package is highlighted and ready to be downloaded.

![](img/ba0161b65b37e94cffc801ecbacaba5e_118_0.png)

To download the package, simply press Enter. You will be asked where you want to save the package. If you started Lynx from your home directory, that is fine for now. Simply press Enter and the package will be downloaded (which could take anywhere from 30 seconds to an hour depending on the speed of your Internet connection). If you didn't start Lynx from your home directory, add ~/ to the beginning of the path to indicate to Lynx that you want to save the file in your home directory.

## Installing the Downloaded Package

When the download has finished, you can exit the Lynx browser by pressing Q. You will be asked if you are sure you want to quit. Press Y and you will be returned to the FreeBSD command prompt. Type ls and you should see the newly downloaded package in the directory list. At the time of this writing, the name of the package was gimp-1.2.3_1,1.tgz. The name of your package may vary slightly depending on what the current version of GIMP is when you read this.

The pkg_add command is used to install new software from packages. Usually, you will have to be the root user to install software packages because they will want to install into directories that normal users do not have write access to. To switch to the root user, you can use the su command. Simply type su and then press Enter. You will be prompted for root's password. After you have typed in the password and pressed Enter, you will have root user privileges, but you will still be located in your same home directory.

In its simplest form, pkg_add can be invoked by simply supplying it with the name of the package file you want to install. For example, to install the GIMP software we downloaded previously, we could simply type

```
pkg_add gimp-1.2.3_1,1.tgz
```

This assumes that you type the command from the directory where the package is currently stored. If you are not in the same directory, you need to supply the directory path to the pkg_add command of where the package is located.

When the package has finished installing, your command prompt will return and you are done. That's all there is to it—even easier than installing software in Windows. Unlike Windows, you will not be prompted for where you want to install the software, and so on because FreeBSD has a strictly enforced policy on where applications are supposed to install their files. Ultimately, this makes for much easier management in the long run because everything will be in a standard location instead of wherever the software programmer decided that the application should install its files.

If you want pkg_add to give you more detail about what it is doing when it installs the software, you can use the -v option, which is short for verbose (for example, pkg_add -v gimp-1.2.3_1,1.tgz).

## Obtaining Information on Installed Packages

FreeBSD maintains a database of all the packages installed on your system. Among other things, this database contains a description of the package, as well as instructions that tell FreeBSD how to uninstall the package if you ever want to do so. You can get a list of packages currently installed on your system by using the pkg_info command. To display all the packages currently installed on your system, use the command pkg_info -a, the -a option being an abbreviation for all. If you just want information on a specific package, you can use the pkg_info command followed by the name of the package. For example, pkg_info gimp-1.2.3_1,1.tgz. If you don't know the exact name of the package you are looking for, you can use the grep command along with a pipe as you learned about in Hour 5, "Advanced UNIX Shell Use." For example,

```
pkg_info -a | grep gimp
```

This command will display all the packages that contain the expression gimp.

You can also use the pkg_info command to display information on a package that is currently not installed by simply supplying it with the location of the package. The location of the package can be either a local directory or an Internet address if the package is located on a remote FTP or Web server.

## Installing Software from Ports

As mentioned previously, the alternative to installing software from prebuilt packages is to install the software from the source code. This system of installing software is known as the ports system. The ports contain information that tells FreeBSD how to build and

# Using XFree86 with MS Windows 9x/2000

To run X Window applications on MS Windows 9x/2000, you need to run an X Window server on such a platform. Many commercial X Window server software packages are available for MS Windows 9x/2000, such as Metro X-Win32, Reflection/X, Exceed, and NTCracker. This section uses Micro X-Win32, which I have used for over a year and find very easy to install and support.

# Getting Micro X-Win32

You can download an evaluation copy of X-Win32 from StarNet Communications Corporation at http://www.starnet.com/. The evaluation version of the product runs exactly like the product version; the only limitation is that you can use the evaluation version for only two hours per session; after every two-hour period, you have to restart the X Window server on the MS Windows side. Because none of the features are crippled in the evaluation version, this constraint is not much of a problem. After all, if you use it, you should pay for it!

After you download an evaluation copy, which typically comes in a self-extracting executable file, extract the files by double-clicking the executable; the installation file will begin automatically. You are asked to select a destination directory for the installation. After it is installed, you are ready to use the X Window server on MS Windows, and your Red Hat Linux server's X client applications can be run on the MS Windows system running the local X Window server.

Before you can run X client from your Red Hat Linux installation, you need to configure Micro X-Win32 using the X-Util32 program provided with the distribution. Do the following:

+   1.  Run the X-Util32 program on a Windows 9x or Windows NT/2000 system.

+   2.  From its menu, select Sessions†Edit sessions. From this menu, select an existing session entry, such as sun. This will display a dialog box with information on the current session.
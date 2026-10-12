+   - Windows 2000
+   - Windows NT
+   - Windows XP
+   - Macintosh

> **NOTE:** In theory, any application that is Win32-compatible should be able to run using software such as WINE (described later). Whether or not a Windows application will run in an emulator in Linux must really be checked on a case-by-case basis.

Emulation programs for running DOS programs are available for Red Hat Linux. You need to install the **dosemu** and/or **xdosemu** packages (which are available from *rmdir.net*). DOS emulation commands from these packages include: *dos*, *xtermdos*, *dosdebug*, *xdos*, and *dosexecc*. Other operating system emulation programs can be added to your system, including:

+   - **WINE**, which lets you run Windows 3.1, Windows 95, Windows 98, Windows 2000, Windows NT, and Windows XP binaries. (Windows NT and XP programs are not well supported.)
+   - **ARDI Executor**, which enables you to run applications that are intended for the Macintosh operating system.

In general, the older and less complex the program, the better chance it has to run in an emulator. Character-based applications generally run better than graphics-based applications. Also, programs tend to run slower in emulation, due sometimes to additional debugging code put into the emulators.

# ## Running DOS applications

Because Linux was originally developed on PCs, a variety of tools were developed to help developers and users bridge the gap between Linux and DOS systems. A set of Linux utilities called *mtools* lets you work with DOS files and directories within Linux. A DOS emulator called **dosemu** lets you run DOS applications within a DOS environment that is actually running in Linux (much the way a DOS window runs within a Windows operating system).

# ## *Using mtools*

*Mtools* are mostly DOS commands that have the letter *m* in front of them and that run in Linux (though there are a few exceptions that are named differently). Using these commands, you can easily work with DOS files and file systems. Table 5-4 lists **mtools** that are available with Linux (if you have the **mtools** package installed).
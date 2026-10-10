5. In the Source Selection Menu, don't select any source packages; just press TAB and then ENTER to update no source packages. (The source packages that can be selected in this menu are unrelated to the ports system.)

6. The system asks if you want to track the FreeBSD ports system. Respond Yes.

7. The system asks if you want to track FreeBSD documentation sources. You can respond either Yes or No, but No will be quicker.

8. The system asks for a base directory. Leave this value at its default (/usr).

9. The system presents a list of CVSup servers. Pick one that's close to you.

10. The system asks if you want to run the update now. Respond No. You should be returned to your shell prompt.

11. Edit the `/etc/cvsupfile` file. This file controls the CVSup process. Comment out any line that begins with `src` – by placing a pound sign (#) at the start of the line. These lines specify core OS source files, which you need not update at this point.

12. Type the following command to update the ports collection:

```
# /usr/local/bin/cvsup -g -L 2 /etc/cvsupfile
```

At this point, the system will update your ports directory tree. You'll see a summary of the retrieved files scroll across your screen, so you can monitor the update's progress. Most updates will happen quickly, but some take more time because the changes are more extensive. Changes to the `ports/INDEX` / `INDEX` file are particularly likely to be lengthy because this file contains information on all the ports on the system. The entire process is likely to take several minutes, and could conceivably take over an hour if your ports collection is particularly out of date or your network connection is slow.

Once you've updated the ports system, you'll have pointers to those packages in your ports tree, but if you've previously installed programs from the ports system, your computer will still have old versions installed. Consult the upcoming section, "Deleting and Upgrading Software," for information on upgrading your already-installed programs.

![](bbox=[0.05, 0.71, 0.93, 0.79])

# Compiling and Installing a Port

The `/usr/ports` directory contains subdirectories relating to specific categories of programs, much like the `sysinstall` Package Selection menu (see Figure 11-1). To install a port, follow these steps:

1. Type `pkg_info -x package-name` to determine whether a package with the name of the port you're installing already exists. If it does, you may not need
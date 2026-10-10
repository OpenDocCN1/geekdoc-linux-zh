+   - **Applications** — This category includes packages of authoring and publishing applications, editors, games, sound and video players, Internet tools, and other applications. (Many of these applications are described in Chapters 5 through 8.)
+   - **Development** — General and specialized software development tools are included in packages in this category.
+   - **Servers** — Packages in this category are for Web, mail, FTP, database, and a variety of other network server types.
+   - **Base System** — Contains basic system administration tools, many common utilities, and support for basic system features (such as X Window System, Java, and Legacy software support).
+   - **Virtualization** — Packages in this category provide virtualization support.
+   - **Cluster** — Packages in this category provide support for cluster computing and administration tools to manage clusters.
+   - **Cluster Storage** — Packages in this category provide support for cluster storage.
+   - **Languages** — Packages containing support for multiple languages are contained in this category.
+      - After you have chosen the packages you want to install, select Next to continue. The installer will take some time to check for dependencies among the packages you selected.

13. **About to Install** — A screen tells you that you are about to begin writing to hard disk. You can still back out now, and your hard disk will not have changed. Click Next to proceed. (To quit without changes, eject the DVD and restart the computer.) Now the file systems are created and the packages are installed. This typically takes from 20 to 60 minutes to complete, although it can take much longer on older computers.

14. **Finish Installing** — When you see the Congratulations screen, you are done. Eject the DVD and click Reboot.

Your computer will restart. If you installed GRUB, you will see a graphical boot screen that gives you several seconds to press a key to view and/or change the bootable partitions. After that, your CentOS installation should boot.

The first time your system boots after installation, CentOS Firstboot runs to do some initial configuration of your system. The next section explains how CentOS Firstboot works.

# Running CentOS Firstboot

The first time you boot CentOS 5, after it is installed, CentOS Firstboot runs to configure some initial settings for your computer.

> **NOTE** Firstboot runs automatically only if you have configured CentOS to boot to a graphical login prompt. To start it from a text login, log in as root and type the following from a Terminal window:
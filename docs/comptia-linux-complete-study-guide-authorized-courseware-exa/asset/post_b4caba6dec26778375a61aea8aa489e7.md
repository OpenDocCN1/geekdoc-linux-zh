
can find the libraries. When this happens, knowing about critical configuration files and commands can help you work around any difficulties.

Beyond managing packages and libraries, Linux software management involves manipulating processes. Knowing how to manipulate foreground and background processes, adjust process priorities, and kill stray processes can help you keep your Linux system working well.

## Exam Essentials

- **Identify critical features of RPM and Debian package formats.** RPM and Debian packages store all files for a given package in a single file that also includes information about what other packages the software depends on. These systems maintain a database of installed packages and their associated files and dependencies.
- **Describe the tools used for managing RPMs.** The `rpm` program is the main tool for installing, upgrading, and uninstalling RPMs. This program accepts operations and options that tell it precisely what to do. The Yum utility, and particularly its `yum` command, enables installation of a package and all its dependencies via the Internet, rather than from local package files.
- **Describe the tools used for managing Debian packages.** The `dpkg` program installs or uninstalls a single package or a group of packages you specify. The `apt-get` utility retrieves programs from installation media or from the Internet for installation and can automatically upgrade your entire system. The `dselect` program serves as a menu-driven interface to `apt-get`, enabling you to select programs you want to install from a text-mode menu.
- **Summarize tools for extracting files and converting between package formats.** The `rpm2cpio` program can convert an RPM file to a `cpio` archive, enabling users of non-RPM systems to access files in an RPM. The `alien` utility can convert in any direction between Debian packages, RPMs, Stampede packages, and tarballs. This enables the use of packages intended for one system on another.
- **Summarize the reasons for using shared libraries.** Shared libraries keep disk space and memory requirements manageable by placing code that’s needed by many programs in separate files from the programs that use it, enabling one copy to be used multiple times. More generally, libraries enable programmers to use basic “building blocks” that others have written without having to constantly reinvent code.
- **Describe methods available to change the library path.** The library path can be changed system-wide by editing the `/etc/ld.so.conf` file and then typing `ldconfig`. For temporary or per-user changes, directories may be added to the path by placing them in the `LD_LIBRARY_PATH` environment variable.
- **Explain the difference between foreground and background processes.** Foreground processes have control of the current terminal or text-mode window (such as an `xterm`). Background processes don't have exclusive control of a terminal or text-mode window but are still running.
- **Describe how to limit the CPU time used by a process.** You can launch a program with `nice` or use `renice` to alter its priority in obtaining CPU time. If a process is truly out of control, you can terminate it with the `kill` command.

## Review Questions

1. Which of the following is not an advantage of a source package over a binary package?
   - A. A single source package can be used on multiple CPU architectures.
   - B. By recompiling a source package, you can sometimes work around library incompatibilities.
   - C. You can modify the code in a source package, altering the behavior of a program.
   - D. Source packages can be installed more quickly than binary packages can.

2. Which is true of using both RPM and Debian package management systems on one computer?
   - A. It’s generally inadvisable because the two systems don’t share installed-file database information.
   - B. It’s impossible because their installed-file databases conflict with one another.
   - C. It causes no problems if you install important libraries once in each format.
   - D. It’s a common practice on Red Hat and Debian systems.

3. Which of the following statements is true about binary RPM packages that are built for a particular distribution?
   - A. They can often be used on another RPM-based distribution for the same CPU architecture, but this isn’t guaranteed.
   - B. They may be used in another RPM-based distribution only when you set the --convert-distrib parameter to rpm.
   - C. They may be used in another RPM-based distribution only after you convert the package with alien.
   - D. They can be recompiled for an RPM-based distribution running on another type of CPU.

4. An administrator types the following command on an RPM-based Linux distribution:
   ```
   # rpm -ivh megaprog.rpm
   ```
   What is the effect of this command?
   - A. The megaprog package, if it’s installed, is uninstalled from the computer.
   - B. The megaprog.rpm package, if it exists, is valid, and isn’t already installed, is installed on the system.
   - C. The megaprog.rpm source RPM package is compiled into a binary RPM for the computer.
   - D. Nothing; megaprog.rpm isn’t a valid RPM filename, so rpm will refuse to operate on this file.

5. Which of the following commands will extract the contents of the `myfonts.rpm` file into the current directory?
   - A. `rpm2cpio myfonts.rpm | cpio -i --make-directories`
   - B. `rpm2cpio myfonts.rpm > make-directories`
   - C. `rpm -e myfonts.rpm`
   - D. `alien --to-extract myfonts.rpm`

6. To use `dpkg` to remove a package called `theprogram`, including its configuration files, which of the following commands would you issue?
   - A. `dpkg -P theprogram`
   - B. `dpkg -p theprogram`
   - C. `dpkg -r theprogram`
   - D. `dpkg -r theprogram-1.2.3-4.deb`

7. Which of the following describes a difference between `apt-get` and `dpkg`?
   - A. `apt-get` provides a GUI interface to Debian package management; `dpkg` doesn't.
   - B. `apt-get` can install tarballs in addition to Debian packages; `dpkg` can't.
   - C. `apt-get` can automatically retrieve and update programs from Internet sites; `dpkg` can't.
   - D. `apt-get` is provided only with the original Debian distribution, but `dpkg` comes with Debian and its derivatives.

8. What command would you type to obtain a list of all installed packages on a Debian system?
   - A. `apt-cache pkgnames`
   - B. `apt-cache showpkg`
   - C. `dpkg -r allpkg`
   - D. `dpkg -i`

9. As *root*, you type `apt-get update` on a Debian system. What should be the effect of this command?
   - A. None; `update` is an invalid option to `apt-get`.
   - B. The APT utilities deliver information about the latest updates you've made to the APT Internet repositories, enabling you to share your changes with others.
   - C. The APT utilities download all available upgrades for your installed programs and install them on your system.
   - D. The APT utilities retrieve information about the latest packages available so that you may install them with subsequent `apt-get` commands.

10. Which of the following commands would you type to update the `unzip` program on a Fedora system to the latest version? (Select all that apply.)
    - A. `yum update unzip`
    - B. `yum upgrate unzip`
    - C. `yum -u unzip`
    - D. `yum -U unzip`

11. How should you configure a system that uses Yum to access an additional Yum software repository?
    - A. Edit the `/etc/apt/sources.list` file to include the repository site's URL, as detailed on the repository's Web site.
    - B. Download a package from the repository site and install it with RPM, or place a configuration file from the repository site in the `/etc/yum/repos.d` directory.
    - C. Use the `add-repository` subcommand to `yum` or the Add Repository option in the File menu in `yumex`, passing it the URL of the repository.
    - D. Edit the `/etc/yum.conf` file, locate the `[repos]` section, and add the URL to the repository after the existing repository URLs.

12. What is the preferred method of adding a directory to the library path for all users?
    - A. Modify the `LD_LIBRARY_PATH` environment variable in a global shell script.
    - B. Add the directory to the `/etc/ld.so.conf` file, and then type `ldconfig`.
    - C. Type `ldconfig /new/dir`, where `/new/dir` is the directory you want to add.
    - D. Create a symbolic link from that directory to one that's already on the library path.

13. You prefer the look of GTK+ widgets to Qt widgets, so you want to substitute the GTK+ libraries for the Qt libraries on your system. How would you do this?
    - A. You must type `ldconfig --makesgqt .gtk`. This command substitutes the GTK+ libraries for the Qt libraries at load time.
    - B. You must uninstall the Qt library packages and re-install the GTK+ packages with the `--substitute=qt` option to rpm or the `--replace=qt` option to dpkg.
    - C. You must note the filenames of the Qt libraries, uninstall the packages, and create symbolic links from the Qt libraries to the GTK+ libraries.
    - D. You can't easily do this; libraries can't be arbitrarily exchanged for one another. You would need to rewrite all the Qt-using programs to use GTK+.

14. A user types `kill -9 11287` at a bash prompt. What is the probable intent, assuming the user typed the correct command?
    - A. To cut off a network connection using TCP port 11287
    - B. To display the number of processes that have been killed with signal 11287 in the last nine days
    - C. To cause a server with process ID 11287 to reload its configuration file
    - D. To terminate a misbehaving or hung program with process ID 11287

15. What programs might you use to learn what your system's load average is? (Select all that apply.)
    - A. `1d`
    - B. `load`
    - C. `top`
    - D. `uptime`

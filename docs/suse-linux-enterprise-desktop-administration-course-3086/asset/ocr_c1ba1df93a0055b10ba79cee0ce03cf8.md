Table 7-4 shows the most important files in a user’s home directory:

| File | Description |
|---|---|
| `.profile` | Private login script of the user |
| `.bashrc` | Configuration file for bash |
| `.bash_history` | List of commands previously run in bash |

# Table 7-4

If there are no special settings, the home directories of all users are located beneath the `/home` directory. The home directory of a user can also be addressed via the shortcut `~`, so `~/.bashrc` refers to the file `.bashrc` in the user’s home directory.

In many cases, the /home directory is located on a different partition or can even be located on a different computer (with central administration of home directories).

# Libraries (/lib)

Many programs use specific functions that are also used by other programs. Such standard functions are removed from the actual program, stored in the system, and only called up when the program runs. They are called *shared libraries*.

The `/lib` directory contains the libraries that are used by programs in the `/bin` and `/sbin` directories. The kernel modules (hardware drivers not compiled into the kernel) are located in the `/lib/modules/` directory.

You can find additional libraries below the directory `/usr`.

# Mountpoints for Removable Media (media/*)

SUSE Linux creates directories in the `/media/` directory for removable media. It creates a separate directory for each kind of media it detects:

+   - `/media/floppy/`—Created for a floppy disk drive.
+   - `/media/cdrom/`—Created for a CD-ROM drive.
+   - `/media/cdrecorder`—Created for a CD burner.
+   - `/media/dvd/`—Created for a DVD drive.
+   - `/media/usbdisk/`—Created for a USB stick.
+   - `/media/medianame`—Created after inserting a labeled removable media.

# Application Directory (/opt)

Installed programs can store their static files in the `/opt` directory. First, a directory with the name of the application is created. The files are then stored in that directory. Examples include GNOME (`/opt/gnome`) and KDE (`/opt/kde3`).
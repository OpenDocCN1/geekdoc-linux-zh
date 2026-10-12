# ## Burning Fedora Core CDs

Linux distributions, including Fedora Core, are available for download from various Internet sites in the form of ISO images — an ISO image is an exact copy of an entire CD-ROM in a single, huge file (typically around 650MB). These files usually have the .iso extension. The ISO part of the name comes from the fact that the CD-ROM uses the ISO 9660 file system and image means the file is an exact replica of every bit of data on the CD-ROM.

In this project, I show you how to burn Fedora Core CDs from the ISO images by using the GnomeToaster application.

# ### Things you need

Here’s what you need to burn the Fedora Core CDs:

+   - A PC running Red Hat Linux or Fedora Core with the X-CD-Roast application installed (consult Book II, Chapter 4 for more information on how to install X-CD-Roast).
+   - An internal or external CD recorder.
+   - Blank CD-R media — you need four blanks for the four-CD Fedora Core.
+   - The downloaded Fedora Core ISO files. If you have not done so already, complete the BitTorrent project and download the four-CD Fedora Core ISO files.

# ### Steps to follow

Follow these steps to use X-CD-Roast to burn the Fedora Core CDs:

+   1. Copy the Fedora Core ISO files to the directory specified in X-CD-Roast as the temporary image storage directory.
+   For example, if you use /tmp as the image storage directory, copy the ISO files to the /tmp directory by using the cp or mv command.
+   2. Choose Main Menu→System Tools→CD Writer from the GNOME or KDE desktop.
+   If you aren’t logged in as root, you’re prompted for the root password. Then the X-CD-Roast main window appears.
+   3. Click Create CD.
+   X-CD-Roast displays the Create CD window.
+   4. Click Write Tracks.
+   X-CD-Roast displays two side-by-side panes: The right pane shows the names of the ISO image files, and the left pane shows what you want to burn on the CD. Initially, the left pane is empty.
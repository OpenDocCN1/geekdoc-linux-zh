# # Immediate Solutions

# ## Installing Perl

Because Perl is not automatically part of Linux, you need to install it before you can program with it. How you install Perl depends on what distribution you are using. These instructions are specific to Red Hat:

+   1. Log in as root.
+   2. Make sure the Red Hat CD-ROM is in the CD-ROM drive.
+   3. Type "mount /mnt/cdrom" to mount the CD-ROM.
+   4. Type "cd /mnt/cdrom/RedHat/RPMS" to change to the packages directory.
+   5. Type "rpm -ihv perl" and press the Tab key to expand the file name, and then press Enter to install the package.
+   6. Type "cd /" to exit the mount point.
+   7. Type "umount /mnt/cdrom" to remove the CD-ROM from your file system.

NOTE: If your distribution does not come with Perl or if you want a newer version, try www.perl.com, www.perl.org, or www.cpan.org. You can get the official source code for the latest release at www.perl.com/CPAN/latest.tar.gz.

# ## Getting And Installing A Perl Library Module

To install a Perl library, do the following:

+   1. Log in as root.
+   2. Use a Web browser to go to www.perl.com/CPAN-local/CPAN.html. The Comprehensive Perl Archive Network (CPAN) is one of the definitive places to go for Perl source code and modules.
+   3. Scroll down to the section with the header "PERL MODULES."
+   4. This is where things get tough, because hundreds of modules are listed. CPAN uses two organizational tools to try to help you find what you need. First, the modules are arranged in alphabetical groups. The second tool is the handy one, however. The modules are arranged in subdirectories
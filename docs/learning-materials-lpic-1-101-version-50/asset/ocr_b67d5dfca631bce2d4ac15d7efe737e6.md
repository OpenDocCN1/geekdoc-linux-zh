# # Guided Exercises

+   1. Imagine a program needs to create a single-use temporary file that will never be needed again after the program is closed. What would be the correct directory to create this file in?
+   
+   2. Which is the temporary directory that *must* be cleared during the boot process?
+   
+   3. Using `find`, search only the current directory for files that are writable by the user, have been modified in the last 10 days and are bigger than 4 GiB.
+   
+   4. Using `locate`, find any files containing both the patterns `report` and either `updated`, `update` or `updating` on their names.
+   
+   5. How can you find where the manpage for `ifconfig` is stored?
+   
+   6. What variable needs to be added to `/etc/updatedb.conf` to make `updatedb` ignore ntfs filesystems?
+   
+   7. A system administrator wishes to mount an internal disk (`/dev/sdc1`). According to the FHS, under which directory should this disk be mounted?
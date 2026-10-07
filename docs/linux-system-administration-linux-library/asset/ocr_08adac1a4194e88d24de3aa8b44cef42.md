# File Characteristics

var is on its own partition;/tmp is often a link to /var/tmp; this frees space on the root partition. The Red Hat distribution uses the tmpwatch command to automatically clean up any file in /tmp or /var/tmp that has not been accessed in 10 days (240 hours). tmpwatch is run from a script in the /etc/cron.daily directory. Chapter 14 for more information on the cron daemon and scripting. The time period may be adjusted as appropriate for your system. The actual command is:

```
/usr/sbin/tmpwatch 240 /tmp /var
```

/usr-MS(mandatory) the /usr directory stores read-only data. Because of this, /usr, if made a separate partition, can be mounted as read-only. To facilitate this, /usr should contain only static data, using links to changeable data in the /var directory to preserve this characteristic.

/var (mandatory) The /var directory contains variable files like logs, and process-specific data files. The existence of a /var directory makes it possible to mount /usr as read-only since files written during system operations are stored in /var instead of in /usr. Since /var contains the system log, /var/log/messages, any problem that sends frequent error messages could fill the /var directory. For this reason, /var is often created on a separate partition from the rest of / to avoid filling up the partition and not being able to log in. It is important to note that not all directories under /var are shareable; /var/log is an example of that which is not.

Of course, anyone with superuser privileges can create directories in /. This is generally to be avoided because the top-level directories were created largely to prevent cluttering up the /. For more information on the underlying directory structure, reference the FSSTND, which may be found at http://www.pathname.com/fhs/

# File Characteristics

The average user, a file is a sequence of information bytes, stored together and named as a collective entity. A file can be an executable program, a document, a database, a shell script, or any other collection of bytes that has meaning. In fact, everything in Linux is seen by the system as a file, including the directories and devices.

Filenames in Linux can range up to 255 characters and may not be terminated with an extension. Filenames are case sensitive, like nearly everything else in Linux. This means that the names File.txt, FILE.txt, file.txt, and File. txt would all refer to different files. The case sensitivity of filenames, combined with their variable length, gives you great flexibility. There are not only more names available to you, but you can use specific capitalization patterns to indicate certain types of files. For instance, you might start directory names with a capital letter.

![](bbox=[0.913, 0.135, 0.978, 0.315])
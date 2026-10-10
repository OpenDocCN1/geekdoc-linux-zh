like should do nicely.) You can then compare this backup to the original file from time to time to be sure you haven’t been compromised. If you do this, though, be sure to do this comparison before updating the Tripwire database, then replace the backed-up file with the new one after making the update.

Tripwire is a useful intrusion detection tool, but it’s most useful if it’s installed immediately after installing and configuring FreeBSD itself. In fact, it’s best to install FreeBSD, configure the system without connecting it to the Internet, install and configure Tripwire, and only then connect the computer to the Internet. This procedure minimizes the risk of compromise before Tripwire’s database is initialized. Unfortunately, Tripwire is most easily installed in FreeBSD as a port, which requires Internet connectivity, so as a practical matter, your best course of action is to make Tripwire installation the first order of business after connecting the system to the Internet. Should you install Tripwire after your computer has been crackerd, Tripwire will happily record the compromised files’ checksums and report no problems.

# Installing Tripwire

When you type **make install** in the Tripwire port directory, in addition to the usual processes, the installer tells you where it will install various binaries, asks for two passphrases for the checksum database (a site passphrase and a local passphrase), and generates an initial checksum database file. Some of these operations can take quite a few minutes, so don’t be alarmed if the computer doesn’t seem to do anything for a while. A large part of this process involves Tripwire’s reading a large number of system files and generating various types of checksums from these files.

> **Note**
> 
> *A passphrase is like a password, but is longer—typically several words. Tripwire uses two passphrases, one to encrypt the policy database file and a second to encrypt the checksum database file.*

When it’s done installing, the Tripwire checksum database resides in the `/var/db/tripwire` directory and is named after the computer on which it runs, such as `wertern.luna.edu.twd`. This file is encrypted and compressed, so it’s unintelligible if viewed with a text editor or file viewer. There are several Tripwire configuration files, all stored in `/usr/local/etc/tripwire`:

+   * `twcfg.txt` This file sets overall options, such as the locations of database files and the method used to send e-mail.
+   * `tw.cfg` Tripwire doesn’t read the `twcfg.txt` file directly; instead, it relies upon a cryptographically signed version of the file, known as `tw.cfg`. This file is encrypted with the site passphrase.
+   * `twpol.txt` Tripwire works by computing several different types of checksums on critical system files and comparing them with stored checksums. The `twpol.txt` policy file describes the files that Tripwire should check and the types of checksums it should compute for each file.
# Using the Recovery Facility

As your computer starts, Ubuntu will show a message prompting you to press Escape to see the GRUB menu. If you do that, you'll see a list of bootable operating systems, which will include Recovery Mode options for your Ubuntu install. If you boot into recovery mode, you'll get automatic root access to your machine which can fix your problems safely.

Alternatively, you can insert your Ubuntu installation disc and use the recovery mode from there. Keep in mind that these recovery modes are designed to be text-only systems for serious system recovery purposes; don't expect them to be hand-held, and don't expect much in the way of ease of use!

# Relevant Ubuntu Commands

The following commands are useful in performing backup, recovery, and restore operations in Ubuntu:

+   - `amanda`—Amanda is a network-based backup system, consisting of 18 separate commands, for use with Linux.
+   - `ark`—A KDE desktop GUI archiving utility.
+   - `cp`—The copy command.
+   - `scp`—The secure shell copy command.
+   - `cpio`—A data archive utility.
+   - `dd`—A data copy and conversion utility.
+   - `gzip`—The GNU compression utility.
+   - `tar`—The GNU tape archive utility.

# Reference

+   - http://www.tldp.org/LDP/solrhe/Securing-Optimizing-Linux-RH-Edition-v1.3/whywhen.html—A thorough discussion with examples of using dump and restore for backups.
+   - http://en.tldp.org/LDP/solrhe/Securing-Optimizing-Linux-RH-Edition-v1.3/chap29sec306.html—Making automatic backups with `tar` using `cron`.
+   - http://kmself.home.netcom.com/Linux/FAQs/backups.html—The Linux Backups mini FAQ contains some useful, although brief, comments on backup media, compression, encryption, and security.
+   - http://www.tldp.org/—The Linux Documentation Project offers several useful HOWTO documents that discuss backups and disk recovery.
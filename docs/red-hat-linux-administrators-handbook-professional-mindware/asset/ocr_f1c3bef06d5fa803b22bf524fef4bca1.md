# Chapter 11

# Sharing Files and Printers with Samba

# Installing Samba

If you chose the DOS/Windows-compatibility option during Red Hat Linux installation, the Samba RPM packages were automatically installed. However, if you did not install Samba packages during installation, you can always install them by using the rpm command. For example, to install the Samba client/server package for an x86 Red Hat Linux system, I ran the following command from the /RedHat/RPMS directory of the official Red Hat CD-ROM:

```
rpm -ivh samba-version.1386.rpm
```

When using this command to install the Samba package, do not forget to replace samba-version.1386.rpm with a real package filename.

# Configuring Samba

When you install the Samba RPM package, it installs a configuration file called smb.conf in your /etc/samba directory. Listing 11-1 shows the default /etc/samba/smb.conf with some minor formatting changes.
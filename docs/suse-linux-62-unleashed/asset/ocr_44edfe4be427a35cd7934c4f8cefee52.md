# Networking and Internet Services
PART II

> Note
You must restart smbd with the following command before your changes take effect:
/etc/rc.d/init.d/smb restart

The SWAT page contains voluminous, well-organized documentation, available even to those not logged in root, and therefore unable to change the configuration.

# Samba Documentation Sources

With SuSE 6.2 installed, you have access to voluminous Samba documentation. Every program has its own man page, available with the Linux command

+   # programname
programname is smbtar, smbmount, or the like.

There is also text-based hyperlink help available with the info program:
#info program
programname is smbtar, smbmount, or the like.

You can find text format Samba documentation in the /usr/doc/packages/samba/textdocs directory. You can find Samba documentation in HTML form in the /usr/doc/packages/samba/htmldocs directory. An excellent SMB HOWTO is located at /usr/doc/howto/en/SMB-HOWTO.gz on your SuSE machine.

As Samba version 2 and later, a greater source of documentation is the SWAT (Samba Administration Tool). SWAT is discussed later in this chapter. If SWAT is enabled on your server, it's a highly organized source of Samba documentation. Users other than root can take advantage of SWAT's documentation, although only user root can alter the smb.configuration through SWAT.

# Samba Applications Documentation Sources

Samba is a suite of programs (listed in Table 16.2) designed to give all necessary client and server access to SMB on your Linux-based computer. Each program has a man page and an info page.
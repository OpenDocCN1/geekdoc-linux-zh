For Samba in NNLS, Novell recommends that you use the Linux User Management (LUM) functionality in iManager to create users.

For more information on the smbpasswd utility, see the smbpasswd man page. Keep in mind, however, the limited function that Novell has specified for this utility in NNLS.

The syntax for the smbpasswd utility is
**/opt/novell/bin/smbpasswd -a username**
where *username* is the LUM username for which you are creating the Samba password.

+   Enable them as Samba users at the same time you **create them in iManager**. This option is available in the same dialog that asks you to LUM enable a user (as shown in Section 4.)

+   Convert them to Samba users after they are created and LUM enabled. This option is available when you convert an eDirectory user to a LUM user in iManager.

If you LUM enable users but opt not to Samba enable them at that time, you can always use iManager or the smbpasswd utility to convert a LUM user to Samba at a later time.

+   Specify and confirm the password.

When a user is Samba enabled, their schema is extended to include a Samba profile. The Samba password is the only value given to the Samba profile.

To avoid confusion, we recommend you use the same password you used for the eDirectory user password.

All users whose accounts have been enabled for Samba access should now be able to access shares on the NNLS server as they would folders on a Windows server.
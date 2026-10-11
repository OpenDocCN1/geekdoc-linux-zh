+   ● Bad Password - Means user logins with an invalid password are treated as a guest login and mapped into the guest account. Note that this can cause problems as it means that any user incorrectly typing their password will be silently logged in as "guest" - and will not know the reason they cannot access files they think they should - there will have been no message given to them that they got their password wrong. Helpdesk services will hate you if you set the map to guest parameter this way :-).

+   ● Bad Uid - Is only applicable when Samba is configured in so some type of domain mode-security (security = {domain ads} ) and means that user logins which are successfully authenticated but which have no valid Unix user account and smbd is unable to create one) should be mapped to the defined guest account. This was the default behavior of Samba 2.x releases. Note that if a member server is running winbindd, this option should never be required, because the nss_winbind library will export the Windows domain users and groups to the underlying OS via the Name Service Switch interface.

Note that this parameter is needed to set up “Guest” share services when using security modes other than share. This is because in these modes the name of the resource being requested is not sent to the server until after the server has successfully authenticated the client so the server cannot make authentication decisions at the correct time (connection to the share) for “Guest” shares.

For people familiar with the older Samba releases, this parameter maps to the old compile-time setting of the GUEST_SESSETUP value in local.h.

# max connections (S) Default: max connections = 010

Example: max connections = 10

This option allows the number of simultaneous connections to a service to be limited. If max connections is greater than 0 then connections will be refused if this number of connections to the service are already open. A value of zero mean an unlimited number of connections may be made.

Record locks are used to implement this feature. The lock files will be stored in the directory specified by the lock directory option.

# max disk size (G) Default: max disk size = 01000

Example: max disk size = 1000

This option allows you to put an upper limit on the apparent size of disks. If you set this option to 100 then all shares will appear to be no larger than 100 MB in size.

Note that this option does not limit the amount of data you can put on the disk. In the above case you could still store much more than 100 MB on the disk, but if a client ever asks for the amount of free disk space or the total disk size then the result will be bounded by the amount specified in max disk size.
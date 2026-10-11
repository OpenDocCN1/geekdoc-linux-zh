# 15.5.6 Interaction with the Standard Samba “create mask” Parameters

There are four parameters that control interaction with the standard Samba *create mask* parameters:

+   * *security mask*
+   * *force security mode*
+   * *directory security mask*
+   * *force directory security mode*

When a user clicks on **OK** to apply the permissions, Samba maps the given permissions into a user/group/world r/w/x triplet set, and then checks the changed permissions for a file against the bits set in the *security mask* parameter. Any bits that were changed that are not set to 1 in this parameter are left alone in the file permissions.

Essentially, zero bits in the *security mask* may be treated as a set of bits the user is *not* allowed to change, and one bits are those the user is allowed to change.

If not explicitly set, this parameter defaults to the same value as the *create mask* parameter. To allow a user to modify all the user/group/world permissions on a file, set this parameter to 0777.

Next Samba checks the changed permissions for a file against the bits set in the *force security mode* parameter. Any bits that were changed that correspond to bits set to 1 in this parameter are forced to be set.

Essentially, bits set in the *force security mode* parameter may be treated as a set of bits that, when modifying security on a file, the user has always set to be *on*.

If not explicitly set, this parameter defaults to the same value as the *force create mode* parameter. To allow a user to modify all the user/group/world permissions on a file with no restrictions, set this parameter to 000. The *security mask* and *force security mode* parameters are applied to the change request in that order.

For a directory, Samba performs the same operations as described above for a file except it uses the parameter *directory security mask* instead of *security mask*, and *force directory security mode* parameter instead of *force security mode*.

The *directory security mask* parameter by default is set to the same value as the *directory mask* parameter and the *force directory security mode* parameter by default is set to the same value as the *force directory mode* parameter. In this way Samba enforces the permission restrictions that an administrator can set on a Samba share, while still allowing users to modify the permission bits within that restriction.

If you want to set up a share that allows users full control in modifying the permission bits on their files and directories and does not force any particular bits to be set *on*, then set the following parameters in the *smb.conf* file in that share-specific section:
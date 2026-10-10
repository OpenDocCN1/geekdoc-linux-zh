To add an object as a trustee to another file or directory, use the command `nwboadstrust`. The new rights you give with this command override any rights that were previously granted explicitly to that object. You must include all three parameters: object, path, and rights mask.

You specify the new rights mask for the user with `RIGHTS_MASK`, which can be a mnemonic or a hexadecimal byte value. To represent the `RIGHTS_MASK` as a mnemonic, enclose the mnemonic inside square brackets using zero or more of the values outlined earlier. To represent the `RIGHTS_MASK` as a hexadecimal byte value, enter the sum of the following hexadecimal values for individual rights:

+   * `00` No access.
+   * `01` Read access.
+   * `02` Write access.
+   * `04` Open access.
+   * `08` Create access.
+   * `10` Delete access.
+   * `20` Ownership access.
+   * `40` Search access.
+   * `80` Modify access.

A total of ff gives all rights.

The syntax is
`nwboadstrust` `-o object` `-r [rights-mask]` `-p object_path`

To give the object `hsimpson` on the bindery server `cburns` all rights to the directory `/users/hsimpson` on the `sys` volume, do the following:
`nwboadstrust` `-o /NetWare/bindery/cburns/objects/hsimpson`
`->r ff` `-d /NetWare/bindery/cburns/volumes/sys/users/hsimpson`

You can also use:
`nwboadstrust` `-o /NetWare/bindery/cburns/objects/hsimpson`
`->r [RWCEMF]` `-d /NetWare/bindery/cburns/volumes/sys/users/hsimpson`

# # Administration for Novell Directory Service

NetWare 4 servers store such essential information as usernames and their group memberships in a special distributed database. This database is the repository of all the

![](bbox=[0.89, 0.3, 0.98, 0.44])
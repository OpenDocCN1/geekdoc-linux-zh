# B.4.21. pgp_path

Default value: (none)

The pgp_path entry is used to point to a directory containing PGP keyring files. These files will be searched for the public key specified by the pgp_name entry.

For more information on signing packages with PGP, see Chapter 17.

# B.4.22. require_distribution

Default value: 0

The require_distribution entry is used to direct RPM to require that every package built must contain distribution information. The default value directs RPM to not enforce this requirement. If the entry has a non-zero value, RPM will only build packages that define a distribution.

# B.4.23. require_icon

Default value: 0

The require_icon entry is used to direct RPM to require that every package built must contain an icon. The default value directs RPM to not enforce this requirement. If the entry has a non-zero value, RPM will only build packages that contain an icon.

# B.4.24. require_vendor

Default value: 0

The require_vendor entry is used to direct RPM to require that every package built must contain vendor information. The default value directs RPM to not enforce this requirement. If the entry has a non-zero value, RPM will only build packages that define a vendor.

# B.4.25. rpmdir

Default value: (topdir)/RPMS

The rpmdir entry is used to define the path to the directory in which RPM will write binary package files. Its default value is taken from the value of the topdir entry, with /RPMS appended to it. Note that if you redefine rpmdir, you'll need to specify a complete path. RPM will automatically add an architecture-specific directory to the end of the path. For example, on an Intel-based system, the actual path would be

```
/usr/src/redhat/RPMS/i386
```
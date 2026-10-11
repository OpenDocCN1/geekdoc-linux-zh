# C.12.1. Options for Add Signature Mode

Only the global options may be used.

# C.13. Check Signature Mode

RPM’s check signature mode is used to verify a package’s signature.

Format:  `rpm --checksig <options> <packagefile>+`

or

`rpm -K <options> <packagefile>+`

# C.13.1. Options for Check Signature Mode

The following option can be used on any check signature command:

+   - `--noglobp`—Skip any PGP signatures (size and MD5 only).

# C.14. Initialize Database Mode

RPM’s initialize database mode is used to create a new RPM database.

Format: `rpm --initdb <options>`

# C.14.1. Options for Initialize Database Mode

Only the global options may be used.

# C.15. Rebuild Database Mode

RPM’s rebuild database mode is used to rebuild an RPM database.

Format: `rpm --rebuilddb <options>`

# C.15.1. Options to Rebuild Database Mode

Only the global options may be used.
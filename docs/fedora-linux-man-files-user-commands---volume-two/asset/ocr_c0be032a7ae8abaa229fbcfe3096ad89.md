and reported **not** to work with `DBD::mysql`. Experimental feature. May not contain double colons (`:`). Default: `SQLite`. See (1).

# gitcvs.dbUser, gitcvs.dbPass

Database user and password. Only useful if setting `gitcvs.dbDriver`, since `SQLite` has no concept of database users and/or passwords. `gitcvs.dbUser` supports variable substitution (see (1) for details).

# gitcvs.dbTableNamePrefix

Database table name prefix. Prepended to the names of any database tables used, allowing a single database to be used for several repositories. Supports variable substitution (see (1) for details). Any non-alphabetic characters will be replaced with underscores.

All `gitcvs` variables except for `gitcvs.usercrlfattr` and `gitcvs.allBinary` can also be specified as `gitcvs.<access_method>.<varname>` (where `access_method` is one of `ext` and `pserver`) to make them apply only for the given access method.

# gitweb.category, gitweb.description, gitweb.owner, gitweb.url

See (1) for description.

# gitweb.avatar, gitweb.blame, gitweb.grep, gitweb.highlight, gitweb.\ patches, gitweb.pickaxe, gitweb.remote_heads, gitweb.showSizes, gitweb.snapshot

See (5) for description.

# grep.lineNumber

If set to true, enable `-n` option by default.

# grep.patternType

Set the default matching behavior. Using a value of `basic`, `extended`, `fixed`, or `perl` will enable the `--basic-regexp`, `--extended-regexp`, `--fixed-strings`, or `--perl-regexp` option accordingly, while the value `default` will return to the default matching behavior.

# grep.extendedRegexp

If set to true, enable `--extended-regexp` option by default. This option is ignored when the `grep.patternType` option is set to a value other than `default`.

# gpg.program

Use this custom program instead of `gpg` found on `$PATH` when making or verifying a PGP signature. The program must support the same command-line interface as `GPG`, namely, to verify a detached signature, `"gpg --verify $file - <$signature"` is run, and the program is expected to signal a good signature by exiting with code 0, and to generate an ASCII-armored detached signature, the standard input of `"gpg -bsau $key"` is fed with the contents to be signed, and the program is expected to send the result to its standard output.
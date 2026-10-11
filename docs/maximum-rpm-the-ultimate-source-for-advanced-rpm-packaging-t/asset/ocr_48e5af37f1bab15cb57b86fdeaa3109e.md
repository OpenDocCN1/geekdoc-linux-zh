# ## C.1. Global Options

The following options can be used in any of RPM's modes:

+   - -quiet—Print as little output as possible.
+   - -v—Be a little more verbose.
+   - -vv—Be incredibly verbose (for debugging).
+   - -root <dir>—Use <dir> as the top-level directory.
+   - -dbpath <dir>—Use <dir> as the directory for the database.
+   - -rcfile <file>—Use <file> instead of /etc/rpmrc and $HOME/.rpmrc.

# ## C.2. Informational Options

The following options are used to display information about RPM:
Format: rpm <option>

+   - -version—Print the version of RPM being used.
+   - -help—Print a help message.
+   - -showrc—Show rcfile information.
+   - -querytags—List the tags that can be used with --queryformat.

# ## C.3. Query Mode

RPM's query mode is used to display information about packages.
Format: rpm --query <options>
or
rpm -q <options>

# ### C.3.1. Package Specification Options for Query Mode

No more than one of the following options may be present in every query command. They are used to select the source of the information to be displayed. Where plus signs appear, more than one item may be included, separated by a space:

+   - <packagename>—Query the named package.
+   - -a—Query all packages.
+   - -f <file>+—Query package owning <file>.
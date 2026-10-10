+   - meld
+   - opendiff
+   - p4merge
+   - tkdiff
+   - tortoisemerge
+   - vimdiff
+   - vimdiff2
+   - vimdiff3
+   - winmerge
+   - xxdiff

# ### merge.verbosity

Controls the amount of output shown by the recursive merge strategy. Level 0 outputs nothing except a final error message if conflicts were detected. Level 1 outputs only conflicts, 2 outputs conflicts and file changes. Level 5 and above outputs debugging information. The default is level 2. Can be overriden by the *GIT_MERGE_VERBOSITY* environment variable.

# ### merge.<driver>.name

Defines a human-readable name for a custom low-level merge driver. See (5) for details.

# ### merge.<driver>.driver

Defines the command that implements a custom low-level merge driver. See (5) for details.

# ### merge.<driver>.recursive

Names a low-level merge driver to be used when performing an internal merge between common ancestors. See (5) for details.

# ### mergetool.<tool>.path

Override the path for the given tool. This is useful in case your tool is not in the *PATH*.

# ### mergetool.<tool>.cmd

Specify the command to invoke the specified merge tool. The specified command is evaluated in shell with the following variables available: *BASE* is the name of a temporary file containing the common base of the files to be merged, if available; *LOCAL* is the name of a temporary file containing the contents of the file on the current branch; *REMOTE* is the name of a temporary file containing the contents of the file from the branch being merged; *MERGED* contains the name of the file to
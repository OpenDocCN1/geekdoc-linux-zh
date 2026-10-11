+   * `$O`—The number of file system outputs.
+   * `$R`—The number of socket messages received.
+   * `$S`—The number of socket messages sent.
+   * `$K`—The number of signals received.
+   * `$C`—The command line.
+   * `$X`—The exit status.

# ## Shell Debugging Options

+   * `-o errexit`—Terminates the shell script if a command returns an error code.
+   * `-o nounset`—Terminates with an error if unset (or non-existent) variables are referenced.
+   * `-o xtrace`—Displays each command before it’s executed.

# ### `shar` Command Switches

+   * `-quiet` (`-silent` or `-q`)—Hides status message while creating archives.
+   * `-intermix-type` (`-p`)—Allows packing options to be applied individually on the command line as opposed to being applied to all files.
+   * `-stdin-file-list` (or `-f`)—Reads a list of files to pack from standard input.
+   * `-output-prefix=s` (or `-o`)—Names of the resulting *shar* files (when used with `-whole-size-limit`).
+   * `-whole-size-limit=k` (or `-l`)—Limits the size of the resulting *shar* files to the specified number of kilobytes, but doesn’t split individual files.
+   * `-split-size-limit=k` (or `-k`)—Limits the size of the resulting *shar* files to the specified number of kilobytes, and splits individual files.
+   * `-archive-name=name` (or `-n`)—Adds an archive name line to the header.
+   * `-submitter=email` (or `-n`)—Adds a *submitted* by line to the header.
+   * `-net-header=s`—Adds *submitted* by and *archive* name headers.
+   * `-cut-mark` (or `-c`)—Adds a `cut here` line for marking the beginning of an archive embedded in the body of an email message.
+   * `-mixed-uencode` (or `-m`)—(default) Allows text and uencoded binary files.
+   * `-text-files` (or `-T`)—Forces all files to be treated as text.
+   * `-uencode` (or `-B`)—Treats all files as binary data to be uencoded.
+   * `-gzip` (or `-z`)—Compresses all data with gzip and uencodes it.
+   * `-level-for-gzip=l` (or `-g`)—Sets the compression level (1–9).
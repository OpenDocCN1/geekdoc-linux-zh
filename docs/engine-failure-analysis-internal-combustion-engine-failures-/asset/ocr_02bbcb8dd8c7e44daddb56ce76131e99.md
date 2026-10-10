# OPTIONS (CONT.)

+   - `-X filename`, `--exclude-from= filename` In a directory comparison, ignore the files and directories specified by the base names in the specified filename.
+   - `--exclude=shell regexp` In a directory comparison, ignore the files and directories specified by *shell regexp* (see the section "Shell Patterns," in Chapter 4).
+   - `-F regexp`, `--show-function-line= regexp` In context and unified format, show portions of the line preceding *regexp* (regular expression).
+   - `-T`, `--initial-tab` In normal or context format, display a tab rather than a space before the text of a line.
+   - `-q`, `--brief` Report only whether the files differ not the details of the differences.
+   - `-s`, `--report-identical-files` Report when two files are the same.
+   - `-l`, `--paginate` Route the output through *pr* to paginate it.
+   - `-v`, `--version` Show the version number.
+   - `-H`, `--speed-large-files` Speed the handling of large files with many scattered small changes.
+   - `-a`, `--text` Treat all files as text and compare them line by line.
+   - `-C [n]`, `--context [ = n ]` Use the context output format,* showing *n* lines (an integer) of context. The default is three lines.
+   - `-y`, `--side-by-side` Use the side-by-side output format.
+   - `-L string`, `--label=string` Use *string* instead of the filename in the context and unified format headers.
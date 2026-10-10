
## General Output Control

- **-c, --count**
  Suppress normal output; instead print a count of matching lines for each input file. With the **-v**, **--invert-match** option (see below), count non-matching lines.

- **--color[=WHEN], --colour[=WHEN]**
  Surround the matched (non-empty) strings, matching lines, context lines, file names, line numbers, byte offsets, and separators (for fields and groups of context lines) with escape sequences to display them in color on the terminal. The colors are defined by the environment variable **GREP_COLORS**. The deprecated environment variable **GREP_COLOR** is still supported, but its setting does not have priority. **WHEN** is **never**, **always**, or **auto**.

- **-L, --files-without-match**
  Suppress normal output; instead print the name of each input file from which no output would normally have been printed. The scanning will stop on the first match.

- **-l, --files-with-matches**
  Suppress normal output; instead print the name of each input file from which output would normally have been printed. The scanning will stop on the first match.

- **-m NUM, --max-count=NUM**
  Stop reading a file after *NUM* matching lines. If the input is standard input from a regular file, and *NUM* matching lines are output, **grep** ensures that the standard input is positioned to just after the last matching line before exiting, regardless of the presence of trailing context lines. This enables a calling process to resume a search. When **grep** stops after *NUM* matching lines, it outputs any trailing context lines. When the **-c** or **--count** option is also used, **grep** does not output a count greater than *NUM*. When the **-v** or **--invert-match** option is also used, **grep** stops after outputting *NUM* non-matching lines.

- **-o, --only-matching**
  Print only the matched (non-empty) parts of a matching line, with each such part on a separate output line.

- **-q, --quiet, --silent**
  Quiet; do not write anything to standard output. Exit immediately with zero status if any match is found, even if an error was detected. Also see the **-s** or **--no-messages** option.

- **-s, --no-messages**
  Suppress error messages about nonexistent or unreadable files.

## Output Line Prefix Control

- **-b, --byte-offset**
  Print the 0-based byte offset within the input file before each line of output. If -o (--only-matching) is specified, print the offset of the matching part itself.

- **-H, --with-filename**
  Print the file name for each match. This is the default when there is more than one file to search.

- **-h, --no-filename**
  Suppress the prefixing of file names on output. This is the default when there is only one file (or only standard input) to search.

- **--label=LABEL**
  Display input actually coming from standard input as input coming from file LABEL. This is especially useful when implementing tools like zgrep, e.g., `gzip -cd foo.gz | grep --label=foo -H something`. See also the -H option.

- **-n, --line-number**
  Prefix each line of output with the 1-based line number within its input file.

- **-T, --initial-tab**
  Make sure that the first character of actual line content lies on a tab stop, so that the alignment of tabs looks normal. This is useful with options that prefix their output to the actual content: -H, -n, and -b. In order to improve the probability that lines from a single file will all start at the same column, this also causes the line number and byte offset (if present) to be printed in a minimum size field width.

- **-u, --unix-byte-offsets**
  Report Unix-style byte offsets. This switch causes grep to report byte offsets as if the file were a Unix-style text file, i.e., with CR characters stripped off. This will produce results identical to running grep on a Unix machine. This option has no effect unless -b option is also used; it has no effect on platforms other than MS-DOS and MS-Windows.

- **-Z, --null**
  Output a zero byte (the ASCII NUL character) instead of the character that normally follows a file name. For example, `grep -IZ` outputs a zero byte after each file name instead of the usual newline. This option makes the output unambiguous, even in the presence of file names containing unusual characters like newlines. This option can be used with commands like `find -print0`, `perl -0`, `sort -z`, and `xargs -0` to process arbitrary file names, even those that contain newline characters.

## Context Line Control

- **-A NUM, --after-context=NUM**
  Print NUM lines of trailing context after matching lines. Places a line containing a group separator (described under `--group-separator`) between contiguous groups of matches. With the `-o` or `--only-matching` option, this has no effect and a warning is given.

- **-B NUM, --before-context=NUM**
  Print NUM lines of leading context before matching lines. Places a line containing a group separator (described under `--group-separator`) between contiguous groups of matches. With the `-o` or `--only-matching` option, this has no effect and a warning is given.

- **-C NUM, -NUM, --context=NUM**
  Print NUM lines of output context. Places a line containing a group separator (described under `--group-separator`) between contiguous groups of matches. With the `-o` or `--only-matching` option, this has no effect and a warning is given.

- **--group-separator=SEP**
  Use SEP as a group separator. By default SEP is double hyphen (`--`).

- **--no-group-separator**
  Use empty string as a group separator.

## File and Directory Selection

- **-a, --text**
  Process a binary file as if it were text; this is equivalent to the `--binary-files=text` option.

- **--binary-files=TYPE**
  If the first few bytes of a file indicate that the file contains binary data, assume that the file is of type TYPE. By default, TYPE is **binary**, and **grep** normally outputs either a one-line message saying that a binary file matches, or no message if there is no match. If TYPE is **without-match**, **grep** assumes that a binary file does not match; this is equivalent to the `-I` option. If TYPE is **text**, **grep** processes a binary file as if it were text; this is equivalent to the `-a` option. *Warning:* **grep** `--binary-files=text` might output binary garbage, which can have nasty side effects if the output is a terminal and if the terminal driver interprets some of it as commands.

- **-D ACTION, --devices=ACTION**
  If an input file is a device, FIFO or socket, use ACTION to process it. By default, ACTION is **read**, which means that devices are read just as if they were ordinary files. If ACTION is **skip**, devices are silently skipped.

- **-d ACTION, --directories=ACTION**
  If an input file is a directory, use ACTION to process it. By default, ACTION is **read**, i.e., read directories just as if they were ordinary files. If ACTION is **skip**, silently skip directories. If ACTION is **recurse**, read all files under each directory, recursively, following symbolic links only if they are on the command line. This is equivalent to the `-r` option.

- **--exclude=GLOB**
  Skip files whose base name matches GLOB (using wildcard matching). A file-name glob can use `*`, `?`, and `[...]` as wildcards, and `\` to quote a wildcard or backslash character literally.

- **--exclude-from=FILE**
  Skip files whose base name matches any of the file-name globs read from `FILE` (using wildcard matching as described under **`--exclude`**).

- **--exclude-dir=DIR**
  Exclude directories matching the pattern `DIR` from recursive searches.

- **-I**
  Process a binary file as if it did not contain matching data; this is equivalent to the **`--binary-files=without-match`** option.

- **--include=GLOB**
  Search only files whose base name matches `GLOB` (using wildcard matching as described under **`--exclude`**).

- **-r**, **`--recursive`**
  Read all files under each directory, recursively, following symbolic links only if they are on the command line. Note that if no file operand is given, `grep` searches the working directory. This is equivalent to the **`-d recurse`** option.

- **-R**, **`--dereference-recursive`**
  Read all files under each directory, recursively. Follow all symbolic links, unlike `-r`.

## Other Options

- **`--line-buffered`**
  Use line buffering on output. This can cause a performance penalty.

- **-U**, **`--binary`**
  Treat the file(s) as binary. By default, under MS-DOS and MS-Windows, **`grep`** guesses the file type by looking at the contents of the first 32KB read from the file. If **`grep`** decides the file is a text file, it strips the CR characters from the original file contents (to make regular expressions with `^` and `$` work correctly). Specifying `-U` overrules this guesswork, causing all files to be read and passed to the matching mechanism verbatim; if the file is a text file with CR/LF pairs at the end of each line, this will cause some regular expressions to fail. This option has no effect on platforms other than MS-DOS and MS-Windows.

- **-z**, **`--null-data`**
  Treat the input as a set of lines, each terminated by a zero byte (the ASCII **NUL** character) instead of a newline. Like the `-Z` or **`--null`** option, this option can be used with commands like **`sort -z`** to process arbitrary file names.

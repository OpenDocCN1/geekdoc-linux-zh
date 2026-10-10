In this statement, pattern specifies the text to match (see the Patterns table in this section), while action is one of the available actions described in Actions table in this section. When gawk reads a text file, it regards each line of text as a record. The built-in variable RS specifies how the record should be broken into sequentially numbered fields ($1, $2, $3, c:.). The built-in variable $0 refers to the whole record.

# OPTIONS

| Use This Option | To Do This |
| --- | --- |
| -F string, --field-separator string | Use string for the input field separator. You can also use a regular expression. |
| -v variable=value | Create variable and assign the indicated value. |
| -i filename --file filename | Read the AWK program source from filename instead of from the first command line argument. |
| -mf n -mr n | Set the mf or mr memory flags to n. |
| -W traditional, -W compat --traditional, --compat | Run in UNIX-AWK compatibility mode. |
| -W copyright, -W copyright --copyright, --copyright | Display the program license. |
| -W help, -W usage, --help, --usage | Show the available options. |
| -W lint, -lint | Provide warnings about constructs that are not portable to other AWK versions. |
| -W lint-old, -lint-old | Provide warnings about constructs that are not portable to the original Unix version of AWK. |
| -W posix, -posix | Enable POSIX compatibility mode. |
| -W re-interval, -re-interval | Enable the use of interval expressions in regular expression matching. |
| -W source program text, --source program text | Use program text as the AWK program source code. |
| -W version, -version | Show the version number. |
| -- | Signal the end of options. |
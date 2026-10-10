# OPTIONS

|
| Use This Option | To Do This |
| :--- | :--- |
| `--retry` | Keep trying to open the file. |
| `-c, --bytes=n` | Output the last n bytes. |
| `#f, --follow[ = \{name|descriptor\} ]` | Output appended data as the file grows. `-f`, `--follow`, and `--follow=` are equivalent. |
| `--help` | Show the available options. |
| `-n, --lines=n` | Output the last n lines instead of the last 10 lines. |
| `--pid=pid` | Terminate after `pid` terminates. |
| `-q, --quiet, --silent` | Suppress the display of filenames. |
| `-s, --sleep-interval=n` | Sleep n seconds after iterations. |
| `-v, --verbose` | Always show filenames. |
| `--version` | Show the version number. |
|

# EXAMPLE

|
| This Command | Does the Following |
| :--- | :--- |
| `tail *.txt` | Prints the last 10 lines of all the `.txt` files in the working directory. Indicates the filename before the output for each file. |
|

# tr

`tr [ option ]` *expression1* [ *expression2* ]

Accept text from the standard input, find the characters matching *expression1* and translate them according to *expression2*. Form the expressions with bracket statements or character classes. You can also use the special characters listed here (see the Special Characters table in this section).
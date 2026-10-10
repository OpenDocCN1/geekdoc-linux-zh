# OPTIONS (CONT.)

| Use This Option | To Do This |
| :--- | :--- |
| `-i` | Provide information only. |
| `-l` | List information about the files being extracted. |
| `-n` *filename* | Use the specified filename. |
| `-q` | Ask for confirmation before extracting files. |
| `-r` | Write resource forks only. |
| `-s` | Write extracted files to standard output in MacBinary format. |
| `-u` | Write data forks only but use Linux line-feed conventions and name the files with the .text suffix. |
| `-U` | Write data forks only but use Linux line-feed conventions. No suffix is added. |
| `-v` | Show all available messages. |
| `-V` | Show the version number. |

# macunpack

macunpack [ option ] filename

Extracts files from a Macintosh MacBinary archive (generally saved with the .bin suffix). By default, the program extracts the files to the working directory and creates subdirectories, if needed, for files saved with path information. This utility is part of the Macutils package, which is available on the following ftp site: meta lab. unc. edu/pub/ linux/utils/compress.

See also hexbin.

# OPTIONS

| Use This Option | To Do This |
| :--- | :--- |
| `-3` | Write files in fork format (info, data, and rsrc). |
| `-a` | Save in AppleShare format in a valid AppleShare folder. |
| `-d` | Write data forks only. |
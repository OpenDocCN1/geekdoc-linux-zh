# # mkdir

**mkdir** [ *option* ] *directory*

Creates the specified directory. To remove a directory, use **rmdir**.

# ## OPTIONS

| Use This Option | To Do This |
| --- | --- |
| --help | Show the available options. |
| -m *mode*, --mode=*mode* | Create the directory with the specified permissions. For information on modes, see the section “Permissions” in this chapter. |
| -p, --parents | Make parent directories as needed. |
| --verbose | Print a message for each directory that is created. |
| --version | Show the version number. |


# ## EXAMPLES

| This Command | Does the Following |
| --- | --- |
| mkdir *essays* | Creates the specified directory ( *essays* ) within the current directory. If the current directory is / *home* / *suzanne*, the created directory is / *home* / *suzanne* / *essays*. |
| mkdir -p *essays* / *english*101 | Creates the specified directory ( *english*101 ) within the *essays* directory. If the *essays* directory (the parent directory of *english*101 ) does not exist, this command creates it. |


# # mkfifo

**mkfifo** [ *option* ] *name*

Creates a pipe with the specified name.
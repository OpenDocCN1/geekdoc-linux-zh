# OPTIONS

| Use This Option | To Do This |
| :--- | :--- |
| -c, --changes | Display messages only when changes are made |
| --dereference | Change the target's ownership rather than the symbolic link's ownership |
| -f, --silent, --quiet | Hide messages |
| -h, --no-dereference | Change symbolic links, not the file to which the symbolic links point |
| --help | Display available options |
| -R, --recursive | Change ownership in the current directory and all of its associated subdirectories |
| --reference=filename | Use the specified filename's owner and group |
| -v, --verbose | Display messages concerning all processed files |
| --version | Display the version number |

# EXAMPLES

| This Command | Does the Following |
| :--- | :--- |
| chown suzanne autobiography.doc | Makes the specified user (suzanne) the owner of auto-biography.doc. |
| chown suzanne.authors essay1.doc | Makes the specified user (suzanne) and the specified group (authors) the owners of essay1.doc. |
| chown -R mike.games * | Makes the specified user (mike) and the specified group (games) the owners of all files in the current directory and all of its associated subdirectories. |

# cp

cp [ option ] [ source ] [ destination ]

Copies one source file (source) to a destination file (destination) or copies multiple source files to a destination that must be an existing
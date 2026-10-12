| Permission | Numeric Equivalent | Description |
| :--- | :--- | :--- |
| drwxr-xr-x | 755 | This directory can be changed only by the owner, but everyone else can view its contents. |
| drwx--x-x | 711 | A combination for keeping a directory world-readable but restricted from access by the ls command. File can be read only by someone who knows the filename. |

**Table 6-2 Common File Permission Descriptions** *(continued)*

# **CRITICAL SKILL**  
**6.5 Managing and Manipulating Files**

This section covers the basic command-line tools for managing files and directories. Most of this will be familiar to anyone who has used a command-line interface. These are the same old functions, but with different command names.

# ## Copying Files: cp

The `cp` command is used to copy files and has a substantial number of options. See its man page for additional details. By default, this command works silently, displaying status information only if an error condition occurs. Here are the most common options for cp:

| Option for cp | Description |
| :--- | :--- |
| `-f` | Force copy; do not ask for verification. |
| `-i` | Interactive copy; before each file is copied, verify with user. |

To copy `index.html` to `index-orig.html`, use the following command:

```
```bash
[michael@workbox michael]$ cp index.html index-orig.html
```
```

To interactively copy all files ending in `.html` to the `/tmp` directory, type this command:

```
```bash
[michael@workbox michael]$ cp -i *.html /tmp
```
```

# ## Moving Files: mv

The `mv` command is used to move files from one location to another. Files can be moved across partitions as well. That requires a copy operation to occur, so such a move may take longer. These are the most common options for `mv`:
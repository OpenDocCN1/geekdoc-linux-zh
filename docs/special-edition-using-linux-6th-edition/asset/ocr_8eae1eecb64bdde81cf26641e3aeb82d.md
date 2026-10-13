| Command | Syntax (Example) | Description |
|---|---|---|
| `gzip` | `gzip <name>` | Compresses a file using Lempel-Ziv coding. Files compressed with this utility have a `.gz` suffix. |
| `gunzip` | `gunzip <name>` | Decompresses a gzipped file. |
| `less` | `less <file>` |  |
|  | `cat <file> \| less` | Similar to the more command but it facilitates backward and forward movement through the file being examined. The name is derived from the saying “Less is more.” |
| `ln` | `ln <source> <dest>` | Used to create hard links between files on the same partition. |
|  | `ln -s <source> <dest>` | Used to create symbolic (or soft) links between files on different partitions or between directories. |
| `lsattr` | `lsattr [option][file]` | Lists the ext2 attribute of the file or directory. |
| `more` | `more <file>` |  |
|  | `cat <file> \| more` | Used to display the contents of a file, one page at a time. |
| `mv` | `mv <source> <dest>` | Used to rename a file. |
| `rm` | `rm <file>` | Removes specified file or files. |
| `tar` | `tar <archive> <files>` | An archive utility. Used to archive or unarchive a set of files. |
|  | `tar -cvf a.tar /etc` | Creates an archive called a.tar that includes the files and directories in the `/etc` directory. |
|  | `tar -xvf a.tar` | Extracts all the files in the a.tar archive. |
| `unzip` | `unzip [options] file` | Compression utility compatible with similar DOS compression utilities that work with ZIP archives. |
| `vi` | `vi <file>` | Full-screen editor. |
| `zip` | `zip [options] <zipfile>` | Creates a ZIP archive. |

# NETWORKING UTILITIES

| Command | Syntax (Example) | Description |
|---|---|---|
| `dig` | `dig <domain>` | Domain information groper. Used to gather information from Domain Name Servers. |
| `dnsdomainname` | `dnsdomainname` | Displays the domain name for the given server. |
| `host` | `host <host>` | Looks up host or host IP address using Domain Name Server. |
| `hostname` | `hostname` | Displays the fully qualified domain name (FQDN) for a server. |
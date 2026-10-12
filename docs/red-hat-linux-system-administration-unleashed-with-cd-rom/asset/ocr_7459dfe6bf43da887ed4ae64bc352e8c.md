# FIGURE 7.1 cfdisk Main Screen.

![](bbox=[0.32, 0.14, 0.86, 0.6])

# TABLE 7.2 cfdisk Command-Line Options

| Option | Description |
|---|---|
| -a | Uses an arrow cursor to indicate the partition instead of the reverse video highlighting. |
| -z | Assumes that the user will be rewriting the entire partition table and skips reading the information from disk. |
| -v | Displays the cfdisk version and copyright and exit. |
| -c cylinders | Specifies the number of cylinders, heads, and sectors instead of using the information supplied by the BIOS to the kernel at boot time. These three options must be used together and are very dangerous. Use with extreme caution. |
| -h heads | Specifies the number of cylinders, heads, and sectors instead of using the information supplied by the BIOS to the kernel at boot time. These three options must be used together and are very dangerous. Use with extreme caution. |
| -s sectors | Specifies the number of cylinders, heads, and sectors instead of using the information supplied by the BIOS to the kernel at boot time. These three options must be used together and are very dangerous. Use with extreme caution. |
| -P opt | Displays information in the format specified by the opt argument, which may be r for raw data format, s for sector order format, or t for raw format. For a complete description of these formats, refer to the cfdisk manual page. |

# Partitioning with sfdisk

As you can see, both the fdisk and cfdisk utilities are easy to use interactively, but if you need the ability to partition a disk in a script, they are of little use. This is the reason for the existence of yet another partitioning utility, sfdisk. This tool, unlike the other two, has a wealth of command-line options as shown in Table 7.4 and takes its input from standard input, making it suitable as the target of a pipeline or for use with a here-document. It can
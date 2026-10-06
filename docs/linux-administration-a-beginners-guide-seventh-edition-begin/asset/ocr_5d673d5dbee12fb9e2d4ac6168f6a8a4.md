# Linux Administration: A Beginner's Guide

| Command-Line Option | Description |
|---|---|n| --force | Tells RPM to forego sanity checks and just do it, even if it thinks you're trying to fit a square peg into a round hole. Be careful with it's the sledgehammer of installation. Typically, you use it when you're knowingly installing an odd or unusual configuration and RPM's safeguards are trying to keep you from doing so. |
| -h | Prints hash marks to indicate progress during an installation. Use with the -v option for a pretty display. |
| --percent | Prints the percentage completed to indicate progress. It's handy if you're running RPM from another program, such as a Perl script, and you want to know the status of the installation. |
| -nodeps | Causes RPM to not perform any dependency checks if RPM is complaining about missing dependency files, but you want the installation to happen anyway. |
| -q | Queries the RPM system for information. |
| --test | Checks to see whether an installation would succeed without performing an actual installation. If it anticipates problems, it displays what they'll be. |
| -V | Verifies RPMs or files on the system. |
| -v | Tells RPM to be verbose about its actions. |

Table 4-2 Common RPM Options (Continued)

# Yum

Yum is one of the more popular packaging/updating tools for managing software on Linux systems. It is basically a wrapper program for RPM, with great enhancements. It has been around for a while, and is now quite mature. Yum has changed and enhanced the traditional approach to package management on RPM-based systems. Popular large sites that serve as repositories for open source software have had to retool slightly to accommodate “Yumified” repositories.
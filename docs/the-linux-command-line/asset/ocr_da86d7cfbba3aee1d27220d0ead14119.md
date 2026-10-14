| Fedora, Red Hat Enterprise Linux, CentOS | rpm | yum |

# Common Package Management Tasks

There are many operations that can be performed with the command line package management tools. We will look at the most common. Be aware that the low-level tools also support creation of package files, an activity outside the scope of this book.

In the discussion below, the term “package_name” refers to the actual name of a package rather than the term “package_file,” which is the name of the file that contains the package.

# Finding A Package In A Repository

Using the high-level tools to search repository metadata, a package can be located based on its name or description.

Table 15-3: Package Search Commands

| Style | Command(s) |
| Debian | apt-get update
apt-cache search search_string |
| Red Hat | yum search search_string |

Example: To search a yum repository for the emacs text editor, this command could be used:

```
yum search emacs
```

# Installing A Package From A Repository

High-level tools permit a package to be downloaded from a repository and installed with full dependency resolution.

Table 15-4: Package Installation Commands

| Style | Command(s) |
| Debian | apt-get update |
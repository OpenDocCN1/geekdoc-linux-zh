# Chapter 5: Accessing and Running Applications

# Using yum-utils package

There are several utilities in the yum-utils package for working with yum repositories and managing software packages. To get these utilities, type the following yum command:

```
# yum install yum-utils
```

These utilities provide different ways of cleaning up repositories, getting packages without installing them, and doing different queries. Here are some examples:

+   - package-cleanup — Check your local RPM database for dependency problems and packages that are not needed. Options include --problems (to check dependency in the RPM database), --orphans (to list packages that are not currently available in any of repositories), and --oldkernels (to remove old kernel and kernel-devel packages). You can add --keepdevel when running --oldkernels, to keep the associated kernel-devel packages.
- repopulse — Check yum repositories for dependency problems. By default, this checks repositories configured for your machine. To check a specific repository, use the -r repoid (option to get the repoid from the first line of the /etc/repos.d file for the repository). Other options include -c file (to use a different configuration file containing repositories) or -a arch (to indicate which base architecture to check for the repository). Note that this command consumes a lot of memory and can take a long time to run.
- downloader — Download a package from a repository to a selected directory. This tool also downloads all dependent along with the requested package by adding the --resolve option. You can specify a download directory (--destdir) or just list the URL where the package would be downloaded from (--) without actually downloading. Use --source to download source packages as well.
- repository — Query yum repositories for information about packages and groups. This command is similar to using rpmquery to query your local RPM database. You can list descriptions of a package (-i), list package dependencies (--requires), and show name, version and release information (-nvr). Type repository --help for other options.

# Getting Fedora and RHEL software updates

With new exploits being discovered daily, any computer connected to the Internet should get regular software updates to patch potential holes and fix broken code. Yum offers several ways of getting updates for Fedora. For Fedora, the GUI utilities for getting updates is called PackageKit.
# SUMMARY

In this chapter, you learned:

+   - Files have three categories to which permissions apply. A file is owned by a user, a single group, and other users. The most specific permission applies. User permissions override group permissions and group permissions override other permissions.
- The ls command with the -l option expands the file listing to include both the file permissions and ownership.
- The chmod command changes file permissions from the command line. There are two methods to represent permissions, symbolic (letters) and numeric (digits).
- The ch command changes file ownership. The -R option recursively changes the ownership of a directory tree.
- The umask command without arguments displays the current umask value of the shell. Every process on the system has a umask. The default umask values for Bash are defined in the /etc/profile and /etc/bashrc files.
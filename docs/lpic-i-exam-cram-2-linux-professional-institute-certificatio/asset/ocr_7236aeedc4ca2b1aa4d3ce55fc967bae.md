removals and can be used only in installation situations for multiple packages on disk. Answer B is incorrect because the **-ea** option does not allow for multiple removals and works only in queries. Answer C is incorrect because there is no **--remove** option for the **rpm** command.

9. You are the system administrator of two firewalls and want to apply updates from a set of packages in the current directory, but you don't want to install any new packages on the systems. In the blank below, enter the exact command with any options and arguments to accomplish this:

The correct answer is **rpm -F \*.rpm**. An alternative answer is **rpm --freshen \*.rpm**.

10. To view the list of required capabilities that a package needs to function properly, which command and options display this for an installed package? Enter only the command and options in the blank below:

The correct answer is **rpm -qR**. An alternative answer is **rpm -q --requires**.
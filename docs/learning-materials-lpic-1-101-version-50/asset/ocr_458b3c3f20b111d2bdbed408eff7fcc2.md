# apt-get update

This command will update the local package index to match what is available within the configured repositories under the `/etc/apt/` directory.

# apt-get install

This command will download a package from a remote repository and install it along with its dependencies, can also be used to install a Debian package that has already been downloaded.

# apt-get remove

This command will uninstall the specified package(s) from the system.

# apt-cache show

Just like the `dpkg -I` command, this command can be used to show details on a specific package.

# apt-cache search

This command will search your local APT cached database for a particular package.

# apt-file update

This command will update the package cache so that the `apt-file` command can query its contents.

# apt-file search

This command will search in which package a file is included. A list of all packages containing the pattern is returned.

# apt-file list

This command is used to list the contents of a package, just like the `dpkg -L` command.
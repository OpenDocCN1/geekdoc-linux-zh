In this example, yum found that gfptf didn't require any additional packages installed. So, typing y at the prompt caused only the one package to be installed.

# Using yum for listing packages

Besides downloading and installing new RPM packages, yum can also be used to list available packages as well as those that are already installed. The following examples illustrate some of uses.

If you want to see a list of all packages that are available for download from the repositories you have configured, type the following:

```
# yum list | less
```

Adding the less command to the end you scroll through the list of software (it could be long, depending on which repositories you point to). If you try to install a package and it fails with a message package xyzypackage needs xyzfile (not provided), you can check for packages including the missing file using the provides option as follows:

```
# yum provides missingfile
```

With the provides option, yum will search your repositories for whatever you enter (instead of missingfile) and return the name of any packages that it finds that file.

To search descriptions in repositories for a particular string, use the search option. For example, the following command searches for arcade in any package description (this search will find some games):

```
# yum search arcade
```

Because yum packages are not automatically deleted after being installed, you might want to go through on occasion and clean them out. To clear out packages from subdirectories of /var/cache/yum directory, type the following:

```
# yum clean packages
```

If you would like to check which RPMs are installed from repositories outside of the main Fedora repository, you can do so using the list extras option. Here is an example:

```
# yum list extras
```

Extra Packages

The list that appears may include a lot of packages, depending on your configuration. Note that this list includes all packages from repositories configured for your system that are outside of Fedora. (For example, it would list packages installed from Livna and ATRPRMS, if those repositories were configured.)
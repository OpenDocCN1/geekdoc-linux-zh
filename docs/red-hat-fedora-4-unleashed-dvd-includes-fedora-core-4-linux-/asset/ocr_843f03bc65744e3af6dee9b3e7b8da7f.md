crash your system. You will be prompted to give confirmation that you want to remove the required package; then Yum processes the packages and their dependencies to remove them safely.

# # Using Yum to Manage Package Inventory

Another useful feature of Yum is the capability to list several sets of packages. There are a few options that you can list, including packages that are currently installed, packages that are available to be installed, and packages that have updates available.

The command is as follows:

```
$ yum list <available> <updates> <installed> <extras>
```

+   - available—This lists the available packages in the configured repositories.
+   - updates—This lists the available updates for currently installed packages.
+   - installed—This lists the packages currently installed on the system.
+   - extras—This lists the installed packages that are not present in any of the configured repositories.

So, if I wanted to find out which packages I have installed on my system, I would use the command `yum list installed` to return a detailed summary of packages installed and their version numbers. You can take this one step further and query for individual packages. You might want to find out which version of OpenOffice.org you have installed and which version is available for installation. For this, you would use `yum list openoffice.org`—the results of which would show you which version was installed and which version was available for updating.

Yum can also search the headers and summaries for each RPM file so you can find specific information about packages that would not usually be available in just the package name itself.

For example, using `yum search kdebindings` would bring up entries matching kdebindings. The results of this command are shown here:

```
$ yum search kdebindings
Searching Packages:
Setting up Repo: dries
Setting up Repo: dag
Setting up Repo: updates-released
Setting up Repo: newrpms
Setting up Repo: freshrpms
Setting up Repo: base
Reading repository metadata in from local files
```
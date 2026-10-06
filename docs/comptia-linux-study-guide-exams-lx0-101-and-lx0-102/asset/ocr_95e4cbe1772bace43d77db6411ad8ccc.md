Search for Packages The search option, noted earlier, searches the database for packages matching the specified name. The result is a list of packages, one per line, with summary codes for each package's install status, its name, and a brief description.

Clean Up the Database The autoclean option removes already-downloaded packages that are no longer available, and clean removes all downloaded packages.

Obtain Help Typing aptitude results in a complete list of options.

Broadly speaking, aptitude combines the interactive features of dselect with the command-line options of apt-get. All three programs provide similar functionality, so you can use whichever you prefer.

A tool's similar to dselect and aptitude in some ways is Synaptic, but Synaptic is a GUI X-based program and is easier to use. Overall, dselect, aptitude, and Synaptic are useful tools, particularly if you need to locate software but don't know its exact name—the ability to browse and search the available packages can be a great boon. Unfortunately, the huge package list can be intimidating.

# Reconfiguring Packages

Debian packages often provide more-extensive initial setup options than do their RPM counterparts. Frequently, the initial script included in the package asks a handful of questions, such as querying for the name of an outgoing mail relay server for a mail server program. These questions help the package set up a standardized configuration that has nonetheless been customized for your computer.

In the course of your system administration, you may alter the configuration files for a package. If you find you have made a mess of things, you may want to revert to the initial standard configuration. To do so, you use the dpkg-reconfigure program, which runs the initial configuration script for the package you specify:

```
# dpkg-reconfigure samba
```

This command reconfigures the samba package, asking the package initial installation questions and restarting the Samba daemons. Once this is done, the package should be closer to its initial state.

# Debian Packages Compared to Other Package Formats

The overall functionality of Debian packages is similar to that of RPMs, although there are differences. Debian source packages are not single files; they're groups of files—the original source tarball, a patch file that's used to modify the source code (including a file that controls the building of a Debian package), and a .desc file that contains a "signature" to help verify the authenticity of the collection. The Debian package tools can combine and compile the package to create a Debian binary package. This structure makes Debian source packages slightly less convenient to transport because you must move at least
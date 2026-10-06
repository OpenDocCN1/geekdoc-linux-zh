# 300 Part III ♦ Choosing and Installing a Linux Distribution

users may depend on these programs to make effective use of the system. The bug tracking and support systems will always include mechanisms for handling these programs when they are provided with the Debian system.

Debian's commitment to free software distribution and openness has earned it a huge following in the technical community. More than any other Linux system, Debian has been used as the basis for other Linux distributions, including KNOPPIX, Damn Small Linux and many others.

The success of Debian has come despite the lack of large corporate sponsors, enterprise initiatives, official certification and training programs. Debian enthusiasts will tell you it is the most stable and reliable Linux system. It is thoroughly tested, and new versions are not released until the Debian leadership believes that story is extraordinarily stable.

# Inside Debian GNU/Linux

Like most modern operating systems, software programs in Debian GNU/Linux are bundled into packages for every distribution and management. The package format and management tools used in Debian GNU/Linux were created by the Debian Project and are arguably the most sophisticated of their type. Additionally, careful adherence to packaging policies and quality-control measures ensure compatibility and help make upgrades smoothly. Debian is one of very few operating system distributions in which all components (except the kernel) can be upgraded without rebooting the system.

# Debian Packages

Debian packages come in two forms: binary and source. Binary packages contain files that are created directly onto the system by the package management tools. Source packages contain source code and build instructions that the Debian build tools use to create binary packages.

In addition to programs and their associated data files, Debian packages contain control data that enable the package management tools to support advanced features:

+   A main control file contains version and package interrelationship data. The version can be compared to an installed version of the same package to determine whether an upgrade is needed. The interrelationship data tell the package management tools which packages must or cannot be installed at the same time as the package.

> Package intersection fields include Depends, Conflicts, Replaces, Provides, Recommends, Suggests, and Enhances. For a complete list of control fields, see http://debian.org/doc/debian-policy/ch-controlfields.html.
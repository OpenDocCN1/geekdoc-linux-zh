# The Linux Softw are Map

The Linux Software Map (LSM) extension .lsm stands off on its own because it is not actually the product of any special tool. Instead, this extension represents a text file following a template provided by the LSM. This template details a set of information about the package, such as the site where new versions can be found and a description of what it is used for.

The actual Linux Software Map is located at www.execpc.com/lsm. Essentially, the LSM is a database of all the software available for Linux. This tool is only as good as the number of programmers who register with it, so if you end up developing programs for Linux, be sure to list them with the LSM.

# Choosing What To Download

Not all programs offer a variety of package choices, but many do. There are pros and cons for each option. Some of these considerations are important under particular situations, whereas others are something you need to consider every time you go to download something.

# Choosing Source, Binary, Or RPM

There are times when you have a choice of what type of format you want to download a program in. Perhaps there is an RPM available on the Red Hat site, but it is not entirely up-to-date. Or perhaps there is no RPM available at all, but you want or need to use the package, and both source code and binary versions are available.

Choosing between these three options—source, binary, or RPM—is sometimes quite straightforward. If an RPM is available and you do not need to make any alterations to the source code, then by all means use the RPM, because Red Hat is an RPM-based distribution. Using an RPM is a good way to ensure that the package is properly entered into the RPM package database so its interactions with other packages can be tracked.

> **NOTE:** *If you are using another distribution that is not based on RPMs, this format should not be your first choice.*

If there is no RPM available but there is a binary available, then many people will try the binary before trying to compile the source. This fact is especially true for those who are not comfortable with programming and compilers.

There are a few reasons to choose source over the other options:

+   - You need to make alterations to the code.
+   - You need to at least look over the code, to see if alterations are necessary. If you do not need to make any changes, you may decide to actually install an RPM or binary instead.
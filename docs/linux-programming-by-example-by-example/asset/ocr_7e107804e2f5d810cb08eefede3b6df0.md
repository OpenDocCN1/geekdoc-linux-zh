The second code block creates a set of directories named after each of the groups defined on your system. Each directory is owned by the default user, but the group ownership is the same as the directory name. All files ending in `*.po` are copied from `src` to the appropriate directory, again setting the group ownership to the directory name and making the files read-only for the owner/ user. No other users or groups have any privileges on these files.

This use of *install* is strange and the file modes, as the listing shows, are unusual, but the example does illustrate why *install* is a better *cp* command and how to use it.

# Using RPM

The Red Hat Package Manager, although it bears Red Hat's name, is a powerful, general, and open software packaging system used by many Linux distributions, including (but not limited to) Caldera's OpenLinux, S.u.S.E., and, of course, Red Hat. It is most frequently used for Linux, but versions of it are available for many UNIX versions, including Solaris, SunOS, HP-UX, SCO, AIX, and Digital UNIX.

The discussion of RPM in this chapter focuses on creating source code packages. If you are interested in mundane issues such as installing, upgrading, and removing RPMs, read Ed Bailey's excellent book, *Maximum RPM*. Point your browser at http://www.rpm.org/ to download the latest version of RPM, to obtain complete documentation, FAQs and HOWTOs, and even to get a downloadable version of the book.

> NOTE
> You are strongly encouraged to purchase *Maximum RPM* and reward both author and publisher for making it freely available. You will likely find that having hard copy is preferable to looking at a soft copy.

# Minimum Requirements

To create RPMs, you need RPM itself, the source code you want to compile, an *rpmrc* file to set some RPM defaults and control its behavior, and a spec file to control the package build process. You should already have a functional development environment (compilers, tools, editors, cold pizza, Jolt cola, coffee, and such) and your source code should compile successfully.

Before proceeding, however, it is essential to convey the mindset behind RPM. RPM always begins with pristine sources. *Pristine*, in this context, means original, unpatched code as it came from the developer. RPM is designed to allow you to apply patches to the original source code. This feature enables you to use RPM to customize software to a specific system or to apply bug fixes.
# CHAPTER FIVE

# Migrating
Solaris Applications to Linux

One of the consequences of the increasing popularity of Linux is that companies are enthusiastic to migrate their existing applications and development environments to Linux. An application following the standards will be easier to port than a nonconformant application. Since Linux and Solaris share the common API sets of UNIX, migrating from Solaris to Linux is easier than from an operating system with different APIs, such as Microsoft Windows.

This chapter provides an outline of the advantages of such a migration and the path that can be taken. In addition to providing the toolkits that can be used in the process of migration, some standard-related porting issues are also discussed.

# 5.1 ROADMAP TO PORT

Developing a portable application is not a easy task. Even though both Solaris and Linux are UNIX variants, there are lots of differences in the APIs, system calls, and other components. Any Linux distribution comes with ample documentation on how to make use of these interfaces to develop applications. However, the documentation is not always clear, and standards are very versatile. One related standard is the Portable Operating System Interface (POSIX) specification (see Section 2.2.1). If you develop your application to be in compliance with this specification, it is much easier to port.

Developing an application for a platform also requires a rich set of tools. Linux as a platform is bundled with many such tools that are open source in nature. These tools include code editors, code formatting tools, compilers,
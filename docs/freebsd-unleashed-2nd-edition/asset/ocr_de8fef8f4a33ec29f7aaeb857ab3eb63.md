# LISTING 14.6 Continued

```
MAINTAINER=    vanilla@FreeBSD.org
GNU_CONFIGURE= yes
USE_GMAKE=    yes

MAN1=         amp.1

do-install:
	@ ${INSTALL_PROGRAM} ${WRKSRC}/amp ${PREFIX}/bin
	@ ${INSTALL_MAN} ${WRKSRC}/amp.1 ${PREFIX}/man/man1
.include <bsd.port.mk>
```

The list of variables tells you what you need to know about where the source for the port comes from, what version the makefile thinks is current, and how to reach the maintainer. The maintainer is a volunteer, usually unaffiliated with whoever develops the actual soft-ware, whose job is to make sure the port compiles and installs cleanly and that the most recent version of the software is reflected in the port.

Most makefiles contain targets, such as clean, install, and all. Not all the makefiles in the ports have these targets, but what they do have is an included central makefile (bsd.port.mk, which lives in the /usr/ports/Mk directory along with other included files). This file is what contains the standardized build targets. The individual makefiles in each port serve as overrides or augmentations (much in the same way /etc/rc.conf relates to /etc/defaults/rc.conf), setting the necessary variables for the build and defining addi-tional targets that will be used in the automated compile process.

# Installing and Removing Ports

Let’s say that a port catches your eye and you decide you want to install it. Here’s where it gets fun. All you have to do is move into the port’s directory (using cd) and type make. This compiles the software. Then, you type make install to install it.

It’s a simple process on the surface, but there’s a lot that goes on under the hood. The make command actually executes a series of sequential make targets (described in Table 14.3). Each one depends on all the previous targets. You can specify any of these targets directly. This will build all targets up to and including the one you specify.

TABLE 14.3 The make Targets in a Port Makefile

| Target | Action |
| :--- | :--- |
| fetch | Downloads the source tarball from the master site into /usr/ports/distfiles |
| checksum | Verifies the authenticity of the tarball using the MDS checksum |
| extract | Unpacks the tarball into a work subdirectory |
| patch | Applies the patches from the files directory to the source |
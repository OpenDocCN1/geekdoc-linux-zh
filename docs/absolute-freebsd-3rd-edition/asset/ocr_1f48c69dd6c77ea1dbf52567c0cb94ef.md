# CSUP, CVSUP, CVS, SUP, AND CTM?

Documentation on the internet unfortunately survives well past reason and rises to sow confusion at the worst possible time. Undead FreeBSD documentation and third-party tutorials might mention using a tool called `CVS` or `CVSup` for source code updates. These tools were replaced in 2013. Any mention of these programs indicates you're reading old docs. If you see a mention of CTM, you're reading docs that predate CVS.4

Upgrading from source requires console access. You won't always need it, but recovering from a bad build might require intervention at the keyboard. Test your serial console, Java app, or IPMI console before installing your home-built operating system version. In my experience, the only upgrades that require console access are those where I don't have console access.

# Which Source Code?

Every FreeBSD release ships with the source code used to build the system you're installing. If you didn't choose to install the source when installing the system, you'll find it on the install media in `/usr/freebsd-dist/src.txz`. If you did install the source code, you'll find it in `/usr/src`.

Unfortunately, this version of the source code lacks the version control tags needed to build FreeBSD. It's for reference only. You'll need to use svnlite(1) to download a version of the code with those tags intact.

Is your copy of source code in `/usr/src` suitable for building FreeBSD? Ask svnlite(1).

```
# svnlite info /usr/src
svn: E155007: '/usr/src' is not a working copy
```
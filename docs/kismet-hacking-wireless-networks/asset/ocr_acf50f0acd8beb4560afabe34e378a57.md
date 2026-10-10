# **WARNING**

In Debian and Slackware distributions (including BackTrack), GpsDrive will not compile correctly without gcc 3.x. Unfortunately, slapt-get does not work correctly out of the box in BackTrack 3 Beta, so you’ll have to do a manual upgrade of gcc (http://gcc.gnu.org/) and then compile GpsDrive. Alternatively, you could simply download a pre-compiled version of GpsDrive.

# Install from Source

To install from source, download the source from the GpsDrive Web site (http://www.gpsdrive.de/). The current stable version (although old) is v2.09. Then:

```
```bash
tar -zxvf gpsdrive-2.09.tar.gz
cd gpsdrive-2.09
./configure
make
make install
```
```

# **NOTE**

If you don’t require support for Garmin’s GPS protocol, configure with the --disable-garmin argument.

# Install from Package

Alternately, you may want to go with a GpsDrive package that is already compiled. Depending upon the distribution you’re using, the package installation procedure may vary. You can find a Slackware-compatible (and BackTrack-compatible) GpsDrive package at http://slackware-current.net/package.php?id=345 (note that this version has Garmin’s GPS protocol already compiled into the package). To install (see Figure 9.5):

```
```bash
installpkg gpsdrive-2.09-i586-1.tgz
```
```
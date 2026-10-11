# ## 11.2. Getting the Sources

The first thing we need to do in order to build a package for cdp\_player is to obtain the sources. Being avid cdp\_player fans from way back, we know that the latest source can be found at GnomoVision\'s FTP site, so we go get a copy.

We now have a gizzpped tar file of cdp\_player version 1.0 on our system. After putting a copy in the SOURCES directory, we're ready to tell RPM what to do with it.

# ## 11.3. Creating the Spec File

The way we direct RPM in the build process is to create a spec file. As we saw in Chapter 10, the spec file contains eight different sections, most of which are required. Let's go through each section and create cdp\_player\'s spec file as we go.

# ### 11.3.1. The Preamble

The preamble contains a wealth of information about the package being built and the people who built it. Here's cdp\_player\'s preamble:

```
# Sample spec file for cdp_player app...
#
Summary: A CD player app that rocks!
Name: cdp\_player
Version: 1.0
Release: 1
Copyright: GPL
Group: Applications/Sound
Source: ftp://ftp.gnomovision.com/pub/cdp\_player/cdp\_player-1.0.tgz
URL: http://www.gnomovision.com/cdp\_player/cdp\_player.html
Distribution: WSS Linux
Vendor: White Socks Software, Inc.
Packager: Santa Claus <sclaus@northpole.com>

%description
It slixes! It dices! It's a CD player app that can't be beat. By using
the resonant frequency of the CD itself, it is able to simulate 20X
oversampling. This leads to sound quality that cannot be equaled with
more mundane software...
```

In general, the preamble consists of entries, one per line, that start with a tag followed by a colon, and then some information. For example, the line starting with **Summary:** gives a short description of the packaged software that can be displayed by RPM. The order of the lines is not important, as long as they appear in the preamble.
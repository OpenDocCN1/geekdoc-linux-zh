Currently the only FRADs supported are the Sangoma Technologies (see http://www.sangoma.com/) 5502A, 5502E and 5508.

To configure the FRAD and DLCI devices after you have rebuilt your kernel, you will need the Frame Relay configuration tools. These are available from ftp://ftp.invlogic.com (see http://ftp://ftp.invlogic.com/pub/linux/fr/frad-0.15.tgz). Compiling and installing the tools is straightforward, but the lack of a top level Makefile makes it a fairly manual process:

```
```
user$ tar xvfz .../frad-0.15.tgz
user$ cd frad-0.15
user$ for i in common dcli frad; do make -C $i clean; make -C $i; done
root# mkdir /etc/frad
root# install -m 644 -o root -g root bin/* ../sm/etc/frad
root# install -m 700 -o root -g root frad/fradcfg $sbin
rppt# install -m 700 -o root -g root dcli/dliccfg $sbin
```
```

Note that the previous commands use *sh* syntax. If you use a *csh* flavor instead (like *tcsh*), the *for* loop will look different.

After installing the tools you need to create an *etc/frad/router.conf* file, you can use this template, which is a modified version of one of the example files:

```
```
# /etc/frad/router.conf

# This is a template configuration for frame relay.
# All tags are included. The default values are based on the code
# supplied with the DOS drivers for the Sangoma S502A card.
#
# A '#' anywhere in a line constitutes a comment
# Blanks are ignored (you can indent with tabs too)
# Unknown [] entries and unknown keys are ignored

[Devices]
Count=1       # number of devices to configure
Dev_1=sd1a0   # the name of a device
#Dev_2=sd1a1 # the name of a device

# Specified here, these are applied to all devices and can be
# overridden for each individual board.

Access=CPE
Clock=Internal
KBaud=64
Flags=TX
```
```
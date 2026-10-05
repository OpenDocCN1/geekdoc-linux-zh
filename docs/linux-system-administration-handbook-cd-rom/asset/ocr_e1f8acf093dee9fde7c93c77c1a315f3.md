# 4.4 AppleTalk

Entries for /etc/services:

```
rtmp  1/ddp # Routing Table Maintenance Protocol
bp   2/ddp # Name Binding Protocol
echo  4/ddp # AppleTalk Echo Protocol
zip    6/ddp # Zone Information Protocol
```

A sample rc.attack:

```
echo -n 'starting appletalk daemons:'
if [ -f /usr/local/atk/etc/atalkd ]; then
    /usr/local/atk/etc/atalkd      echo -n ' atalkd'
```

```
if [ -f /usr/local/atk/bin/nbprstr ]; then
    /usr/local/atk/bin/nbprstr -p 4 'hostname|sed 's/..*//'
  `Workstation`
```

```
if [ -f /usr/local/atk/bin/nbprstr ]; then
    /usr/local/atk/bin/nbprstr -p 4 'hostname|sed 's/..*//'
  `netatalk`                      echo -n ' nbprstr'
```

```
if [ -f /usr/local/atk/etc/papd ]; then
    /usr/local/atk/etc/papd      echo -n ' papd'
```

```
if [ -f /usr/local/atk/etc/afpd ]; then
    /usr/local/atk/etc/afpd       echo -n ' afpd'
```

AppleVolumes.system provides a filename for type mapping. Also carriage return to line feed mapping is controlled in this file. Typically altering file extensions for which translation is the only reason you would need to edit this file.

AppleVolumes.default contains a list of directories and optional labels to be exported as Appleshares. If the label is present, it will be used to identify the volume in the chooser and desktop. The tilde (~) in this file will tell the server to present the user's home directory in the list of exported volumes.
A sample AppleVolumes.default:

```
# This file looks empty when viewed with "vi*". In fact, there is one
# '~', so users with no AppleVolumes file in their home directory get
# their home directory by default.
```
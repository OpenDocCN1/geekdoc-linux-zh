-2 Uses format 2 for the dump

'begin' and 'size' can have the following format:

x[k|m|b|t|c]

for x byte, kilobyte, megabyte, blocks, tracks, and cylinders

+   - `-i` Prints general DASD information and geometry
+   - `-x` Prints extended DASD information
+   - `-j` Prints the volume serial number (volume identifier)
+   - `-l` Prints information about the volume label
+   - `-t` Prints the table of contents (VTOC)
+   - `-h` Prints this usage text
+   - `-v` Prints the version number
+   - `-n` Specifies the device by a device number (needs devfs)
+   - `-f` Specifies a device by a device node

Two examples of the dasdview command are shown in Figure 6-3 and Figure 6-4 on page 215.

```
# dasdview -i /dev/dasda
--- general DASD information ----------------
device node : /dev/dasda
busid : 0.0.9144
type : ECKD
device type : hex 3390 dec 13200
--- DASD geometry ---------------------------
number of cylinders : hex d0b dec 3339
tracks per cylinder : hex f dec 15
blocks per track : hex c dec 12
blocksize : hex 1000 dec 4096
```

Figure 6-3 dasdview command with the -i option
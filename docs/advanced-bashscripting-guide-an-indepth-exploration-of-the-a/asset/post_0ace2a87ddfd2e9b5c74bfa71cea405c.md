
## Chapter 29. Zeros and Nulls

/dev/zero and /dev/null

### Uses of /dev/null

Think of /dev/null as a "black hole". It is the nearest equivalent to a write-only file. Everything written to it disappears forever. Attempts to read or output from it result in nothing. Nevertheless, /dev/null can be quite useful from the command line and in scripts.

Suppressing stdout or stderr (Example 12-2):

```bash
rm $badname 2>/dev/null
# Error messages [stderr] deep-sided.
```

Deleting contents of a file, while preserving the file itself, with all attendant permissions (from Example 2-1 and Example 2-2):

```bash
cat /dev/null > /var/log/messages
# : > /var/log/messages has same effect, but does not spawn a new process.
cat /dev/null > /var/log/tmp
```

Automatically emptying the contents of a logfile (especially good for dealing with nasty "cookies" sent by Web sites):

### Example 29-1. Hiding the cookie jar

```bash
[ -f ~/.netscape/cookies ] # Remove, if exists.
then
  rm -f ~/.netscape/cookies
  ln -s /dev/null ~/.netscape/cookies
fi
# All cookies now sent to a black hole, rather than saved to dev.

### Uses of /dev/zero

Like /dev/null, /dev/zero is a pseudo file, but it actually contains nulls (zeros, not the ASCII character). When written to it, it disappears, and it is difficult to read the nulls in /dev/zero, though it can be done with od or a hex editor. The chief use for /dev/zero is in creating an initialized dummy file intended as a temporary swap file.

### Example 29-2. Setting up a swapfile using /dev/zero

```bash
#!/bin/bash

# Creating a swapfile.
# This script must be run as root.
ROOT_UID=0 # Root has $UID 0.
```

 Advanced Bash–Scripting Guide

```bash
E_WRONG_USER=65    # Not root?

FILE=~/swap
BLOCKSIZE=1024
MINBLOCKS=40
SUCCESS=0

if [ "$UID" -ne "$ROOT_UID" ]
then
    echo; echo "You must be root to run this script."; echo
    exit E_WRONG_USER
fi

if [ -n "1" ]
then
    blocks=$1
else
    blocks=$MINBLOCKS    # Set to default of 40 blocks
                         # if nothing specified on command line.
fi

if [ "$blocks" -lt $MINBLOCKS ]
then
    # Must be at least 40 blocks long.
fi
```

Another application of /dev/zero is to "zero out a file of a designated size for a special purpose, such as mounting a filesystem on loopback device (see Example 13–6) or securely deleting a file (see Example 12–36).

### Example 29–3. Creating a ramdisk

```bash
#!/bin/bash
# ramdisk.sh

# A "ramdisk" is a segment of system RAM memory
# that acts as if it were a filesystem.
# Its advantage is very fast access (read/write time).
# Disadvantages: volatility, loss of data on reboot or overpower.
#                 less RAM available to system.

# What is a good ramdisk?
# Keeping a large dataset, such as a table or dictionary on ramdisk
# speeds up data lookup, since memory access is much faster than disk access.

E_NON_ROOT_USER=70                # Must run as root.
ROOTUSER_NAME=root
```

 Advanced Bash-Scripting Guide

```bash
MOUNTTP=/mnt/ramdisk
SIZE=2000                          # 2K blocks (change as appropriate)
BLOCKSIZE=1024                      # 1K (1024 byte) block size
DEVICE=/dev/ram0                    # First ram device

username=$(id -nu)
if [ "$username" != "$ROOTUSER_NAME" ]
then
    echo "Base must be run as \"$(basename $0)\"."
    exit $E_NON_ROOT_USER
fi

if [ ! -d "$MOUNTTP" ];               # Test whether mount point already there,
then
    mkdir $MOUNTTP                    # so no error if this script is run
                                     # multiple times.
fi

dd if=/dev/zero of=$DEVICE count=$SIZE bs=$BLOCKSIZE  # Zero out RAM device.
mke2exts $DEVICE                     # Create ext2 filesystem on it.
mount $DEVICE $MOUNTTP                # Mount it.
chmod 777 $MOUNTTP                   # So ordinary user can access ramdisk.
                                     # However, must be root to unmount it.

echo "\"$MOUNTTP\" now available for use."
# The ramdisk is now accessible for storing files, even by an ordinary user.

# Caution, the ramdisk is volatile, and its contents will disappear
# on reboot or power loss.
# Copy anything you saved to a regular directory.

# After reboot, run this script again to set up ramdisk.
# Remounting /mnt/ramdisk without the other steps will not work.
```

exit 0

## Chapter 30. Debugging

The Bash shell contains no debugger, nor even any debugging-specific commands or constructs. Syntax errors or outright typos in the script generate cryptic error messages that are often of no help in debugging a non-functional script.

### Example 30–1. A buggy script

```bash
#!/bin/bash
# ex74.sh

# This is a buggy script.

a=37

if [ $a -gt 27 ]
then
  echo $a
fi

exit 0
```

Output from script:

```
./ex74.sh: [37]: command not found
```

What's wrong with the above script (hint: the **if**)?

What if the script executes, but does not work as expected? *This is all the too familiar logic error.*

### Example 30–2. test24, another buggy script

```bash
#!/bin/bash
# This is supposed to delete all filenames in current directory
# containing embedded spaces.
# It doesn't work. Why not?

badname=$(ls | grep ' ')
# echo "$badname"
```

# Advanced Bash-Scripting Guide

```
rm -f ~/.netscape/cookies

ln -s /dev/null ~/.netscape/cookies
#All cookies now get sent to a black hole, rather than saved to disk.
```

Uses of /dev/zero
Like /dev/null,/dev/zero is a pseudo-device file, it actually produces a stream of nulls (binary zeros, not the ASCII kind). Output to /dev/zero disappears, and it is fairly difficult to actually produce the nulls emitted there, though it can be done with od or a hex editor. The use of /dev/zero is creating an initializing dummy file of predetermined length intended as a temporary swap file.

# Example 31-2. Setting up a swapfile using /dev/zero

```
#!/bin/bash
# Creating a swap file.

# A swap file provides a temporary storage cache
#+ which helps up certain filesystem operations.

ROOT_UID=0              # Root has SUID 0.
E_WRONG_USER=85       # Not root?

FILE=swap
BLOCKSIZE=1024
MINBLOCKS=40
SUCCESS=0

# This script must be run as root.
if [ "$SUID" -ne "$ROOT_UID" ]
then
echo; echo "You must be root to run this script."; echo
exit $E_WRONG_USER
fi

blocks=${1:-$MINBLOCKS}      # Set to default of 40 blocks
#+ if in nothing specified on command-line.
# This is the equivalent of the command block below.

if [ -n "$1" ]
then
blocks=$1
else
blocks=$MINBLOCKS
fi
```

```
if [ "$BLOCKS" -lt $MINBLOCKS ]
then
blocks=$MINBLOCKS      # Must be at least 40 blocks long.
nfi
```

```
######################################################################
echo "Creating swap file of size $blocks blocks (KB)."  # Zero out out file.
diff if=/dev/zero of=$FILE bs=$BLOCKSIZE count=$blocks
```

Chapter 31. Of Zeros and Nulls
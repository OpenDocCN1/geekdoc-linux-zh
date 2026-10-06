
# Advanced Bash–Scripting Guide

```bash
#!/bin/bash
# Capture keystrokes without needing to press ENTER.

keypresses=4                              # Number of keypresses to capture.

old_tty_setting=$(tty -g)                # Save old terminal settings.
echo "Press $keypresses keys."         # Disable canonical mode.
stty -icanon -echo                       # Disable local echo.
keys=$(dd bs=1 count=$keypresses 2>/dev/null)    # 'dd' uses stdin, if "if" not specified.

stty "$old_tty_setting"               # Restore old terminal settings.
echo "You pressed the $keys"

# Thanks, S.C. for showing the way.
exit 0
```

The dd command can read raw data on a data stream.

```bash
echo -n | dd bs=1 seek=4 of=file conv=noctrunc
# The "conv=noctrunc" option means that the output file will not be truncated

# Thanks, S.C.
```

The dd command copy raw data and disk images to and from devices, such as floppies and tape drives (Example A-5). A common use is creating boot floppies.

```bash
dd if=kernel-image of=/dev/fd0H1440
```

Similarly, dd can copy the entire contents of a floppy, even one with a "foreign" OS, to the raw hard drive as an image.

```bash
dd if=/dev/fd0 of=...img
```

Other applications of dd include initializing temporary swap files (Example 29–2) and ramdis (Example 29–3). It can do a low-level copy of an entire drive partition, although this is not necessarily recommended.

People who have nothing better to do (with their time) are constantly thinking of interesting applications of dd.

# Example 12–36. Secure deleting a file

```bash
#!/bin/bash
# blotout.sh: Erase all traces of a file.
# This script overwrites a target file alternately
## with random bytes, zeros before finally deleting it.
# After that, even examining the raw disk sectors
## will not reveal the original file data.

PASSES=7
# Number of file-shredding passes.
BLOCKSIZE=1
# I/O with /dev/urandom requires unit block size,
# otherwise you get weird results.
E_BADARGS=70
E_NOT_FOUND=71
E_CHANGED_MIND=72

if [ -z "$1" ]; then  # No filename specified.
then
    echo "Usage: basename $0 filename"
    exit $E_BADARGS
fi

file=1

if [ ! -e "$file" ]; 
then
    echo "File $file not found."
    exit $E_NOT_FOUND
fi

echo; echo -n "Are you absolutely sure you want to blot out $file? (y/n) "
read answer
case "$answer" in
[nN]) echo "Changed CHANGED_MIND, huh?"
    exit $E_CHANGED_MIND
    ;
*) echo "Blotting out $file.";
    break
esac

flength=$(ls -1 "$PASSES") | awk '{print $5}'  # Field 5 is file length.

pass_count=1

echo

```bash
while [ "$pass_count" -le "$PASSES" ];
do
    echo "$pass_count"
# Flush buffers.
    sync
    dd if=/dev/urandom of=$file bs=$BLOCKSIZE count=$flength
    # Fill with random bytes.
    sync
    # Flush buffers again.
    dd if=/dev/zero of=$file bs=$BLOCKSIZE count=$flength
    # Fill with zeros.
    sync
    # Flush buffers yet again.
    let "$pass_count += 1"
done
```

```bash
rm -f $file  # Finally, deleted scrambled and shredded file.
sync
# Flush buffers out a final time.
```

echo "File $file blotted out and deleted."; echo

# # This is a fairly secure, if inefficient and slow method
# of thoroughly "shredding" a file. The 'shred' command,
## part of the GNU "fileutils" package, does the same thing,
# but more efficiently.

# The file cannot be "undeleted" or retrieved by normal methods.
# However...
# this simple method will likely *not* withstand forensic analysis.

## Tom Vier's "wipe" file-deletion package does a much thorough job
# of file shredding than this simple script.
# http://www.ibibio.org/pub/Linux/utils/file/wipe-2.0.0.tar.bz2

# For an in-depth analysis on the topic of file deletion and security,
## see Peter Gutmann's paper,
# "Secure Deletion of Data From Magnetic and Solid-State Memory"
# http://www.cs.auckland.ac.nz/~-pgut01/secure_del.html

exit 0
```

## 12.9. Miscellaneous Commands

The **od**, octal dump file converts (or files) to text (base-8) or other bases. This is useful for viewing or processing binary data files or other bases. This is useful for viewing or processing binary data files or other bases. This is useful for viewing or processing binary data files or other bases.

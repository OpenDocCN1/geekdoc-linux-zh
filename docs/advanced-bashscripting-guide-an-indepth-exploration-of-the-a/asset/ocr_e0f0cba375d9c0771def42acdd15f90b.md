# Chapter 29. Zeros and Nulls

/dev/zero and /dev/null

Uses of /dev/null

Think of /dev/null as a "black hole". It is the nearest equivalent to a write-only file. Everything written to it disappears forever. Attempts to read or output from it result in nothing. Nevertheless, /dev/null can be quite useful from the command line and in scripts.

Suppressing stdout or stderr (Example 12-2):

```
rm $badname 2>/dev/null
# Error messages [stderr] deep-sided.
```

Deleting contents of a file, while preserving the file itself, with all attendant permissions (from Example 2-1 and Example 2-2):

```
cat /dev/null > /var/log/messages
# : > /var/log/messages has same effect, but does not spawn a new process.
cat /dev/null > /var/log/tmp
```

Automatically emptying the contents of a logfile (especially good for dealing with nasty "cookies" sent by Webcom sites):

# Example 29-1. Hiding the cookie jar

```
[ -f ~/.netscape/cookies ] # Remove, if exists.
then
rm -f ~/.netscape/cookies

ln -s /dev/null ~/.netscape/cookies
# All cookies now sent to a black hole, rather than saved to dev.
```

Uses of /dev/zero

Like /dev/null, /dev/zero is a pseudo file, but it actually contains nulls (zeros, not the ASCII character). When written to it, it disappears, and it is difficult to read the nulls in /dev/zero, though it can be done with od or a hex editor. The chief use for /dev/zero is in creating an initialized dummy file intended as a temporary swap file.

# Example 29-2. Setting up a swapfile using /dev/zero

```
#!/bin/bash

# Creating a swapfile.
# This script must be run as root.
ROOT_UID=0 # Root has $UID 0.
```

Chapter 29. Zeros and Nulls
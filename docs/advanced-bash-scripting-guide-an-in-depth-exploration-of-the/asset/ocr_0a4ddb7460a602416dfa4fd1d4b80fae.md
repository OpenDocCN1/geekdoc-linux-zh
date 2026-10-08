# Advanced Bash-Scripting Guide

```
#! /bin/bash
# blank-name.sh
# Substitutes underscores for blanks in all the filenames in a directory.

ONE=1 # For getting singular/plural right (see below).
number=0 # Keeps track of how many files renamed.
FOUND=0 # Successful return value.

for filename in *; #Traverse all files in directory.
do
    echo "$filename" | grep -q " " # Check whether filename
    if [ $? -eq $FOUND ]; then # + counts spaces(s)
    ethen
        fname=$filename # Yes, this filename works.
        n=$(echo $filename | sed -e "s/ /_/g") # Substitute underscore for blank.
        mv "$filename" "$n" # Do the actual renaming.
        let number=$number + 1
    fi
done

if [ "$number" -eq "ONE" ]; # For correct grammar.
then
    echo "$filename file renamed."
else
    echo "$filename files renamed."
fi
```

Example A-4. encryptedpw: Uploading to an ftp site, using a locally encrypted password

```
#!/bin/bash

# Example ex72.sh modified to use encrypted password.

# Note that this is still rather insecure,
+# since the decrypted password is sent in the clear.
# Use something like "ssh" if this is a concern.

E_BADARGSS=85

if [ -z "$1" ];
then
    echo "Usage: basename $0 filename"
    exit $E_BADARGSS
fi

Username=bozo # Change to suit.
pword=/home/bozo/secret/password_encrypted.file
# File containing encrypted password.

Filename=$(basename $1) # Strips pathname out of file name.

Server=XXXnDirectory=YYY # Change above to actual server & directory.

Password=$<cruft # Decrypt password.
# Uses the author's own "cruft" file encryption package,
+# based on the classic "onetime pad" algorithm.
```

# Appendix A. Contributed Scripts

579
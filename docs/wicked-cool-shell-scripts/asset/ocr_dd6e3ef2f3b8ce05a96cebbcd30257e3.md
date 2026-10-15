# The Code

```
#!/bin/bash

# ftpget--Given an ftp-style URL, unwraps it and tries to obtain the
# file using anonymous ftp

anonpass="$LOGNAME@$(hostname)"

if [ $# -ne 1 ] ; then
 echo "Usage: $0 ftp://..." >&2
 exit 1
fi

# Typical URL: ftp://ftp.ncftp.com/unixstuff/q2getty.tar.gz

if [ "$(echo $1 | cut -c1-6)" != "ftp://" ] ; then
 echo "$0: Malformed url. I need it to start with ftp://" >&2
 exit 1
fi

server="$(echo $1 | cut -d/ -f3)"
filename="$(echo $1 | cut -d/ -f4-)"
basefile=$(basename $filename)

echo "$0: Downloading $basefile from server $server

ftp -np << EOF
open $server
user ftp $anonpass
get "$filename" "$basefile"
quit
EOF

if [ $? -eq 0 ] ; then
 ls -l $basefile
fi

exit 0
```

Listing 7.1: The ftpget script

# How It Works

The heart of this script is the sequence of commands fed to the FTP program starting at 1. This illustrates the essence of a batch file: a sequence of instructions that’s fed to a separate program so that the receiving program (in this case FTP) thinks the instructions are being entered by the user. Here we specify the server connection to open, specify the anonymous user
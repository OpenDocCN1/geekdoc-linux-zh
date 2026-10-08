```
#!/bin/csh
#   Program to test file $1

if (-e $1) then
	echo "$1 exists"
else
	echo "$1 does not exist"
endif

if (-z $1) then
	echo "$1 is zero length"
else
	echo "$1 is not zero length"
endif

if (-f $1) then
	echo "$1 is a file"
else
	echo "$1 is not a file"
endif

if (-d $1) then
	echo "$1 is a directory"
else
	echo "$1 is not a directory"
endif

if (-o $1) then
	echo "you own $1"
else
	echo "you don't own $1"
endif

if (-r $1) then
	echo "$1 is readable"
else
	echo "$1 is not readable"
endif

if (-w $1) then
	echo "$1 is writable"
else
	echo "$1 is not writable"
endif

if (-x $1) then
	echo "$1 is executable"
else
	echo "$1 is not executable"
endif
```
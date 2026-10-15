if_demo3 file, as shown in the following session. As you can see, although it contains more functionality, it is more elegant than the previous two versions.

```
% cat if_demo3
#!/bin/csh
if ( ( $#argv == 0 ) || ( $#argv > 1 ) ) then
    echo "Usage: $0 ordinary_file"
else if ( ! -e $1 ) then
    echo "$1 : non-existent file"
else if ( -d $1 ) then
    set nfiles = `ls $1 | wc -w`
    if ($nfiles == 0) then
        echo "$1 : Empty directory"
    else
        echo "The number of files in $1 is : $nfiles."
    endif
else if ( -f $1 ) then
    set filename = $argv[1]
    set fileinfo = `ls -il $filename`
    set inode = $fileinfo[1]
    set perms = $fileinfo[2]
    set size = $fileinfo[6]
    echo "File Name:      $filename"
    echo "Inode Number:   $inode"
    echo "Permissions:    $perms"
    echo "Size (bytes):   $size"
else
    echo "$0: argument must be an ordinary file"
endif
% ./if_demo3
Usage: if_demo3 ordinary_file
% ./if_demo3 lab1
lab1 : non-existent file
% ./if_demo3 dir1
dir1 : Empty directory
% ./if_demo3 .
The number of files in . is : 17.
% ./if_demo3 lab3
File Name:      lab3
Inode Number:   4313
Permissions:    -rw-r--r--
Size (bytes):   221
%
```

If the command line argument is an existing file, the required file-related data is displayed. If the argument is a directory, the number of files in it (including directories and hidden files) is saved in the nfiles variables and displayed. If the argument is a
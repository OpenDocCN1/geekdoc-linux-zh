![](bbox=[0.32, 0.12, 0.78, 0.58])

FIGURE 14.2 Semantics of the if-then-else-endif statement.

```
endif
if ( -d $1 ) then
    echo "$1 : directory"
    echo "Usage: $0 ordinary_file"
    exit 1
endif
if ( -f $1 ) then
    set filename = $argv[1]
    set fileinfo = `ls -il $filename`
    set inode = $fileinfo[1]
    set perms = $fileinfo[2]
    set size = $fileinfo[6]
    echo "File Name:        $filename"
    echo "Inode Number:     $inode"
    echo "Permissions:      $perms"
    echo "Size (bytes):     $size"
    exit 0
else
    echo "$0: argument must be an ordinary file"
    exit 1
endif
%
```

The third version of the if statement is used to implement multiway branching. The following is a brief description of the statement.
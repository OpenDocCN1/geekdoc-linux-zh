# 14.2.1.2. find-provides: Automatically Determine Shared Library Sonames

The `find-provides` script for Linux is a bit more complex, but still pretty straightforward:

```
#!/bin/bash

# This script reads filenames from STDIN and outputs any relevant
# provides information that needs to be included in the package.

filelist=$(grep "\.so" | grep -v "^/lib/ld.so" | xargs file -L 2>/dev/null | grep 'ELF.*shared object' | cut -d: -f1)

for f in $filelist; do
    soname=$(objdump -p $f | awk '/SONAME/ {print $2}')
    if [ "$soname" != "" ]; then
        if [ ! -L $f ]; then
            echo $soname
        fi
    else
        echo ${f##*/}
    fi
done | sort -u
```

First, a list of shared libraries is created. Then, for each file on the list, the soname is extracted and cleaned up, and duplicates are removed.

# 14.2.2. Automatic Dependencies: An Example

Let’s take a widely used program, `ls`, the directory lister, as an example. On a Red Hat Linux system, `ls` is part of the `fileutils` package and is installed in `/bin`. Let’s play the part of RPM during `fileutils`’s package build and run `find-requires` on `/bin/ls`. Here’s what we’ll see:

```
# find-requires
/bin/ls
<ctrl-d>
libc.so.5
#
```

The `find-requires` script returned `libc.so.5`. Therefore, RPM should add a requirement for `libc.so.5` when the `fileutils` package is built. We can verify that RPM did add `ls`’s requirement for `libc.so.5` by using RPM’s `--requires` option to display `fileutils`’s requirements:

```
# rpm -q --requires fileutils
libc.so.5
#
```

Okay, that’s the first half of the equation: RPM automatically detecting a package’s shared library requirements. Now let’s look at the second half of the equation: RPM detecting packages that provide shared libraries. Since the `libc` package includes, among others, the shared library `/lib/libc.so.5.3.12`, RPM would obtain its soname. We can simulate this by using `find-provides` to print out the library’s soname:

```
# find-provides
/lib/libc.so.5.3.12
```
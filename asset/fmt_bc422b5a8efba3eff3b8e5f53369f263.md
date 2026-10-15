
```
Subject: Warning: ashley Exceeds Quota

Your disk usage is 539.7MB, but you have been allocated only 500MB. This means that you need to delete some of your files, compress your files (see ‘gzip’ or ‘bzip2’ for powerful and easy-to-use compression programs), or talk with us about increasing your disk allocation.

Thanks for your cooperation in this matter.

Your friendly neighborhood sysadmin
```

Listing 5-5: The email sent to the `ashley` user for being a disk hog

## Hacking the Script

A useful refinement to this script would be to allow certain users to have larger quotas than others. This could easily be accomplished by creating a separate file that defines the disk quota for each user and setting a default quota in the script for users not appearing in the file. A file with account name and quota pairs could be scanned with `grep` and the second field extracted with a call to `cut -f2`.

## 37 Improving the Readability of df Output

The `df` utility output can be cryptic, but we can improve its readability. The script in Listing 5-6 converts the byte counts reported by `df` into more human-friendly units.

### The Code

```
#!/bin/bash

# newdf--A friendlier version of df

awkscript="/tmp/newdf.$$"

trap "rm -f $awkscript" EXIT

cat << 'EOF' > $awkscript
function showunit(size) {
  mb = size / 1024; prettymb=(int(mb * 100)) / 100;
  gb = mb / 1024; prettygb=(int(gb * 100)) / 100;

  if ( substr(size,1,1) != "[0-9]" || substr(size,2,1) != "[0-9]" ) { return size }
  else if ( mb < 1 ) { return size "K" }
  else if ( gb < 1 ) { return prettymb "M" }
  else { return prettygb "G" }
}

BEGIN {
  printf "%-7s %10s %7s %7s %8s %-s\n",
    "Filesystem", "Size", "Used", "Avail", "Capacity", "Mounted"
}

//Filesystem/ {

size=showunit($2);
used=showunit($3);
avail=showunit($4);

printf "%-7s %10s %7s %7s %8s %-s\n",
  $1, size, used, avail, $5, $6
}
```

EOF

```
df -k | awk -f $awkscript
```

exit 0

Listing 5-6: The `newdf` script, wrapping `df` so it is easier to use

### How It Works

Much of the work in this script takes place within an `awk` script, and it wouldn't take too big of a step to write the entire script in `awk` rather than in the shell, using the `system()` function to call `df` directly. (Actually, this script would be an ideal candidate to rewrite in Perl, but that's outside the scope of this book.)

There's also an old-school trick in this script at ① and ② that comes from programming in BASIC, of all things.

When working with arbitrary-precision numeric values, a quick way to limit the number of digits after the decimal is to multiply the value by a power of 10, convert it to an integer (dropping the fractional portion), and then divide it by the same power of 10: `pretty_mb=(int(mb * 100)) / 100;`. With this code, a value like 7.085344324 becomes a much more attractive 7.08.

> NOTE
>
> Some versions of `df` have an `-h` flag that offers an output format similar to this script's output format. However, as with many of the scripts in this book, this one will let you achieve friendly and more meaningful output on every Unix or Linux system, regardless of what version of `df` is present.

### Running the Script

This script has no arguments and can be run by anyone, root or otherwise. To avoid reporting disk use on devices that you aren't interested in, use `grep -v` after the call to `df`.

### The Results

Regular `df` reports are difficult to understand, as shown in Listing 5-7.

```
$ df
Filesystem      512-blocks   Used   Available Capacity Mounted on
/dev/disk0s2    935761728 628835600 306414128  68%    /
devfs           375         375     0         100%   /dev
map -hosts      0           0       0         100%   /net
map auto_home   0           0       0         100%   /home
localhost:/mnt/Yw... 935761728 935761728 0       100%   /Volumes/MobileBackups
```

Listing 5-7: The default output of `df` is convoluted and confusing.

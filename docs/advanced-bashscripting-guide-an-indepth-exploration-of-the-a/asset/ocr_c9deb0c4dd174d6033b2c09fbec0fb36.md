# Advanced Bash-Scripting Guide

```
zz=0 # == Temp variable, keeping track of directory level.
while [ $zz -le $depth ]; do # Keep track of inner nested loop.
  echo -n "| " # == Display vertical connector symbol,
  zz=$((zz+1)) # == Increment with 2 spaces & no free line in order to indent.
done
  if [ -L "$dir" ]; then # == If directory is a symbolic link...
    echo "---$dir" | ls -ld "$dir" | sed 's/^/  /'
    # == Display list header. and directory name, but...
    # == Display date/time of long listing.
  else
    echo "---$dir" # == Display horizontal connector symbol...
    # == and print directory name.
    if cd "$dir"; then # == If move to subdirectory...
      depth=$((depth+1)) # == Increment depth.
      search # == Function calls itself.
      numdirs=$((numdirs+1)) # == Increment count.
    fi
  fi
fi
done
  cd .. # == Up one directory level.
  if [ $depth -eq 0 ]; then # == If depth = 0 (returns TRUE)...
    swfi1=1 # == set flag showing that search is done.
  fi
  depth=$((depth-1)) # == Decrement depth.
done
# - Main -
if [ $# -eq 0 ]; then
  cd "$PWD"
  cd "$PWD" # == No arguments to script, then use current working directory.
else
  cd $1 # == Otherwise, move to indicated directory.
fi
echo "Initial directory = $PWD"
swfi0=0 # == Search finished flag.
deep0=0 # == Depth of listing.
numdirs0=0
zz0=0
while [ $swfi0 -ne 1 ]; do # == While flag not set...
  search # == Call function after initializing variables.
done
echo "Total directories = $numdirs"
```

exit 0
# ==> Challenge: try figuring out exactly how script works.

Noah Friedman gave permission to use this string script, which essentially reproduces some of the C-library string manipulation functions.

# Appendix A–16. string functions: C–like string functions

```
#!/bin/bash
# string.bash -- bash emulation of string(3) library routines
```

Appendix A. Contributed Scripts
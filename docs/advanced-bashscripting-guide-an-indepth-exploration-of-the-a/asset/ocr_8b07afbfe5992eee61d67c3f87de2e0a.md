# Advanced Bash–Scripting Guide

+   * Put files containing your favorite and most useful definitions and functions. As necessary, "include" one or more of these "library files" in scripts with either the dot (.) or source command.

```
# SCRIPT LIBRARY
#

# Note:
# No "!" here.
# No "live code" either.

# Useful variable definitions
ROOT_UID=0      # Root has UID 0.
E_NOTROOT=101 # Not root user error.
MAXRETVAL=256 # Maximum (positive) return value of a function.
SUCCESS=0
FAILURE=-1

# Functions
Usage ()       # "Usage:" message.
{
  if [ -z "$1" ] # No arg passed.
  then
    msg=filename
  else
    msg=$0
  fi
}
echo "Usage: $(basename $0)\ "$msg"
```

```
Check_if_root () # Check if root is running script.
if [ "$UID" -ne "$ROOT_UID" ] # From "ex39.sh" example.
then
  echo "Must be root to run this script"
  exit E_NOTROOT
fi

CreateTempFileName () # Creates a "unique" temp filename.
{
  prefix=temp
  suffix=$(date +%s)
  Tempfilename=$prefix.$suffix
}

isalpha2 () # Tests whether "entire string" is alphabetic.
{
  # From "isalpha.sh" example.
  if [ $1 -eq 1 ] || return $FAILURE
}
case $1 in
  "*[a-zA-Z]*") return $FAILURE;
  *) return $SUCCESS;
```

# 34.4. Optimizations

317
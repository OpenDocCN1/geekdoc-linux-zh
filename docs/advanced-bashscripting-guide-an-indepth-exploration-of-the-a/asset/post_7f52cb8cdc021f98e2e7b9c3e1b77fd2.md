
# Advanced Bash–Scripting Guide

```
SITE=`domainname`.toronto.edu
# ==> `domainname` similar to 'hostname'
# ==> May rewrite this to parameterize for this general use.

usage="Usage: $0 [-h remotehost] [-d remotirectory]... [-f remfile:localfile] ... \
  [-c localdirectory] [-m filename] [-v]"
ftpflags="i -n*"
varflag=""
set x="# So we use globbing in -m*"
set x 'getopts d:ic:f:'
if [ $? -ne 0 ]; then
    echo "$usage"
    exit 65
fi
shift
trap 'rm -f "$TMPFILE"; exit 0 1 2 3 15' EXIT
echo "user anonymous ${USER-gnu}@${SITE}" > ${TMPFILE}
# ==> Added quotes (recommended in complex echoes)
echo binary >> ${TMPFILE}
for i in $@
do
    case $i in
        -v) varflag=-v; echo hash >> ${TMPFILE}; shift;
        -h) remothost=$2; shift 2;
        -d) echo cd $2 >> ${TMPFILE};
            if [ "$varflag" != "$x" ]; then
                echo passwd >> ${TMPFILE};
            fi;
            shift 2;
        -c) echo cd $2 "$2" >> ${TMPFILE}; shift 2;
        -f) fi-expr="$2" = "([^[::]]**"; f2="$2" = "[[::]]*(:.+)"
            echo get $($f2) >> ${TMPFILE}; shift 2;
        *) break;
    esac
done
if [ $# -ne 0 ]; then
    echo $usage
    exit 65 # ==> Changed from "exit 2" to conform with standard.
fi
if [ "$varflag" != "$x" ]; then
    ftpflags="${ftpflags}-v"
fi
if [ "$remhost" = "" ]; then
    remotep=prep.ai.mit.edu
    # ==> Rewrite to your favorite ftp site.
fi
echo quit >> ${TMPFILE}
# ==> All commands saved in template.

tftp ${ftpflags} ${remhost} < ${TMPFILE}
# ==> Now, tempfile batch processed by ftp.

rm -f ${TMPFILE}
# ==> Finally, deleted template (you may wish to copy it to a logfile).

# ==> Exercises:
# ==> 1) Add error checking.
# ==> 2) Add bells & whistles.
```

Appendix A. Contributed Scripts

# Advanced Bash–Scripting Guide

Antek Sawicki created the following script, which makes very clever use of the parameter substitution operators discussed in Section 9.3.

# Example A–12. password: Generating random 8-character passwords

```
#!/bin/bash
# !/bin/bash2 on older machines.
# May need to be invoked with
# Random password generator for bash 2.x by Antek Sawicki <tenox@tenox.tc,
# who generously gave permission to the document author to use it here.
# --> Comments added by document author -->

MATRIX="0123456789ABCDEFGHIJKQRSTUVWXYZabcdefghijklmmnopqrstuvwxyz"
LENGTH=${#MATRIX}

while [ $n -le 1 ]; do
# - is "default substitution" operator.
# Recall that if 'n' has not been initialized, set it to 1.
do
  PASS=$SPASS${($RANDOM%${#MATRIX})):1}
  # --> Very clever, but tricky.

  # --> Starting from the innermost nesting...
  # --> ${#MATRIX} returns length of array MATRIX.
  # --> ${RANDOM%${#MATRIX}} returns random number between 1
  # --> and length of MATRIX - 1.

  PASS=$SPASS{($RANDOM%${#MATRIX})):1}
  # --> returns expansion of MATRIX at random position, by length 1.
  # --> See (var:pos:len) parameter substitution in Section 3.3.1
  # --> and following examples.
  PASS=$PASS... simply pastes this rest onto previous PASS (concatenation).
  # --> To visualize this more clearly, uncomment the following line
  # --> echo "$SPASS"
  # --> to see PASS building up,
  # --> one character at a time, each iteration of the loop.
  let n+=1
  # --> Increment 'n' for next pass.
done

echo "$SPASS"

# --> Or, redirect to file, as desired.
```

James R. Van Zandt contributed this script, which used names and, in his words, "really exercises quoting and escaping.",

# Advanced Bash–Scripting Guide

# Example A–13. Making daily backups, using named pipes

```
#!/bin/bash
# ==> Script by James R. Van Zandt, and used here with his permission.

# ==> Comments added by author of this document.

HERE=$(uname -n)  ==> hostname
THERE-bilbo
echo "starting remote backup to $(date +%r)"
# ==>  date +%r returns time in 12-hour format, i.e. "08:08:34 PM".

# make sure /pipe really is a pipe and not a plain file
rm -f /pipe
mkfifo /pipe
# ==>  Create a "named pipe", named "pipe"

# ==> 'uyz' runs commands as user "uyz"
# ==> 'ssh' invokes commands (remote login).
su uyz -c "ssh $HERE < /home/uyz/backup/$HERE.tar.gz>" > /pipe
# ==> Uses named pipe, /pipe, to communicate between processes:
# ==> 'tar' writes to /pipe and 'ssh' reads from /pipe.

# The result backs up the main directories, from down.

# ==> What are the advantages of a "named pipe" in this situation,
# as opposed to "anonymous pipe", with
# ==> Will anonymous pipe work here?

exit 0

Stephane Chelas contributed the following script to demonstrate generating numbers require arrays.

# Example A–14. Generating prime numbers using modulo operator

```
#!/bin/bash
# primes.sh: Generate prime numbers, without arrays.
# Script contributed by Stephane Chelas.

# This does "not" use the classic "Eratosthenes" algorithm,
# This does "not" use the classic "Eratosthenes" algorithm,
# but instead uses more intuitive method of testing each candidate (divisors), using modulo operator.

LIMIT=1000

Primes()
  (( n = $1 + 1 ))
  # Bump to next integer.
  shift
  # Next parameter in list.
  echo -n=$n
  if (( n == LIMIT ))
  then
    echo $*
    return
  fi

  for i; do
    echo -n=$n $i
    (( n % i == 0 )) && continue
    Primes $n
  return
done

Primes 1

# "i" gets set to previous values of $n
# Optimization.
# Sift out non-primes modulo operator.
# Recursion inside loop.
# Recursion outside loop.
# Successively accumulate positional parameters.
# is the accumulating list of primes.

Uncomment lines 17 and 25 to figure out what is on.

Compare the speed of this algorithm for generating primes
with Sieve of Eratosthenes (primes.sh).
# Exercise: Rewrite this script without recursion, for faster execution.

Jordi Sanelas gave permission to use his elegant tree script.

# Example A–15. Displaying a directory tree

```
#!/bin/sh
# tree by Jordi Sanelas email: mikaku@arrakis.es
# Initial version: 1.0
# Next version: 1.1

search () {
  for dir in 'echo *
  # 'echo *' lists all the files in working directory, without line breaks.
  # Similar effect to for dir in *
  # but dir in 'echo *' will not handle filenames with blanks.
  do
    if [ -d "$dir" ]; then # If it is a directory (-d)
      zz=0 # Temp variable, keeping track of directory level.
      while [ $zz -le $depth ]; do # Keep track of nested loop.
        echo -n "| " # Display vertical connector symbol,
        zz=$((zz+1)) # Increment with 2 spaces & no free line in order to indent.
      done
      if [ -L "$dir" ]; then # If directory is a symbolic link...
        echo "---$dir" | ls -ld "$dir" | sed 's/^/  /'
        # Display list header. and directory name, but... Display date/time of long listing.
      else
        echo "---$dir" # Display horizontal connector symbol...
        # and print directory name.
        if cd "$dir"; then # If move to subdirectory...
          depth=$((depth+1)) # Increment depth.
          search # Function calls itself.
          numdirs=$((numdirs+1)) # Increment count.
        fi
      fi
    fi
  done
    cd .. # Up one directory level.
    if [ $depth -eq 0 ]; then # If depth = 0 (returns TRUE)...
      swfi1=1 # set flag showing that search is done.
    fi
    depth=$((depth-1)) # Decrement depth.
  done
}
# - Main -
if [ $# -eq 0 ]; then
  cd "$PWD"
  cd "$PWD" # No arguments to script, then use current working directory.
else
  cd $1 # == Otherwise, move to indicated directory.
fi
echo "Initial directory = $PWD"
swfi0=0 # Search finished flag.
deep0=0 # Depth of listing.
numdirs0=0
zz0=0
while [ $swfi0 -ne 1 ]; do # While flag not set...
  search # Call function after initializing variables.
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

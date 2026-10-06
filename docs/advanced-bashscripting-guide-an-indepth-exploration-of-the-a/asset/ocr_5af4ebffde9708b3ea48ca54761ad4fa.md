# Chapter 33. Scripting With Style

Get into the habit of writing shell scripts in a structured and systematic manner. Even "on–the-fly" and "written on the back of an envelope" scripts will benefit if you take a few minutes to plan and organize your thoughts before sitting down coding.

Herewith a few stylistic guidelines. This is not intended as an Official Shell Scripting Stylesheet.

# 33.1. Unofficial Shell Scripting Stylesheet

+   * Comment your code. This makes it easier to understand (and appreciate), and easier for you to maintain.
* PASS="$PASSES(MATRIX:$($RANDOM$(#MATRIX))):):1"
* It made perfect sense when you wrote it last year, but now it's a complete mystery.
* (From Anton Sawicki's "pw.sh" script.)

Add descriptive headers to your scripts and functions.

```
#!/bin/bash

****************************************************
# xyz.sh
# written by Bozo Bozman
# July 05, 2001

# Clean up project files.
****************************************************

BADDIR=65      # No such directory.
projectdir=/home/bozo/projects  # Directory to clean up.

####################################################
cleanup_files() {
# Removes all files in designated directory
# Parameter: $target_directory
# Returns: 0 on success, $BADDIR if something went wrong.
####################################################
cleanup_files() {
  if [ ! -d "$1" ]; # Test if target directory exists.
  then
    echo "$1 is not a directory."
    return $BADDIR
  fi

  rm -f "$1"*      # Success.
  return 0
}

cleanup_files $projectdir

exit 0
```

Be sure to put the #!/bin/bash at the beginning of the first line of the script, preceding any comment headers.
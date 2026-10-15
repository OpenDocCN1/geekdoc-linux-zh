web administrator is the traverse function (enabled using -traversal), which causes lynx to try to step through all links on a site to see if any are broken. This feature can be harnessed in a short script, as Listing 9-1 details.

# The Code

```
#!/bin/bash
# checklinks--Traverses all internal URLs on a website, reporting
# any errors in the "traverse.errors" file

# Remove all the lynx traversal output files upon completion.
trap "$(which rm) -f traverse.dat traverse2.dat" 0

if [ -z "$1" ]; then
  echo "Usage: checklinks URL" >&2
  exit 1
fi

baseurl=$(echo $1 | cut -d/ -f3 | sed 's/http:\/\//')"

lynx -traversal -accept_all_cookies -realm "$1" > /dev/null

if [ -s "traverse.errors" ]; then
  /bin/echo -n "$wc -l < traverse.errors" errors encountered.
  echo Checked $(grep '^http' traverse.dat | wc -l) pages at ${1}:
  sed "s|$1|g" < traverse.errors
  mv traverse.errors ${baseurl}.errors
  echo "A copy of this output has been saved in ${baseurl}.errors"
else
  /bin/echo -n "No errors encountered.";
  echo Checked $(grep '^http' traverse.dat | wc -l) pages at ${1}
fi

if [ -s "reject.dat" ]; then
  mv reject.dat ${baseurl}.rejects
fi

exit 0
```

Listing 9-1: The checklinks script

# How It Works

The vast majority of the work in this script is done by lynx; the script just fiddles with the resulting lynx output files to summarize and display the data attractively. The lynx output file reject.dat contains a list of links pointing to external URLs (see Script #70 on page 220 for how to exploit this data), traverse.errors contains a list of invalid links (the gist of this script), traverse.dat contains a list of all pages checked, and traverse2.dat is identical to traverse.dat except that it also includes the title of every page visited.
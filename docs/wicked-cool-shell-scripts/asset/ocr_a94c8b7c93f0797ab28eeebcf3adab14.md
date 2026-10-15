```
while [ $# -gt 0 ]
do
case $1 in
/D ) flags="$flags -x" ;; 
/H ) usage ;; 
/[NQW] ) flags="$flags -l" ;; 
/OD ) flags="$flags -rt" ;; 
/O-D ) flags="$flags -t" ;; 
/P ) postcmd="more" ;; 
/S ) flags="$flags -s" ;; 
* ) # Unknown flag; probably a DIR specifier break;
    # so let's get out of the while loop.
esac
shift    # Processed flag; let's see if there's another.
done

# Done processing flags; now the command itself:
if [ ! -z "$postcmd" ] ; then
ls $flags "$@" | $postcmd
else
ls $flags "$@"
fi

exit 0
```

Listing 2.17: The DIR shell script for emulating the DIR DOS command on Unix

# How It Works

This script highlights the fact that shell case statement conditional tests are actually regular expression tests. You can see at 8 that the DOS flags /N, /Q, and /W all map to the same -l Unix flag in the final invocation of the ls command and that all this is done in a simple regular expression /[NQW].

# Running the Script

Name this script DIR (and consider creating a system-wide shell alias of dir=DIR since DOS was case insensitive but Unix is most assuredly case sensitive). This way, whenever users type DIR at the command line with typical MS-DOS DIR flags, they'll get meaningful and useful output (shown in Listing 2-18) rather than a command not found error message.

# The Results

```
$ DIR /OD /S ~/Desktop
total 48320
7720 PERP - Google SEO.pdf          28816 Thumbs.db
0 Traffic Data                      8 desktop.ini
8 gofathershood-com-crawlerrors.csv 80 change-lid-close-behavior-win7-1.png
16 top-100-errors.txt               176 change-lid-close-behavior-win7-2.png
0 $RECYCLE.BIN                      400 change-lid-close-behavior-win7-3.png
```
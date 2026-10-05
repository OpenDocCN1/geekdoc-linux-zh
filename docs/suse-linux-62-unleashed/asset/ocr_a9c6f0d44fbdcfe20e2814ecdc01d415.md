# LISTING 22.2 CONTINUED

BEFORE=$1
AFTER=$2

+   # Toss the BEFORE and AFTER arguments out of the argument list.
shift;shift;

```
for FILE in $*
do
    sed -e "s/$BEFORE/$AFTER/*" $FILE > $TMPFILE
    echo "$FILE"
    diff $FILE $TMPFILE
    echo ""
    mv $TMPFILE $FILE
done
```

Most interactive editors permit a form of global search-and-replace, and some even make it easy to operate on more than one file. Perhaps that's a superior automation for your needs. If not, chstr is a minimal command-line alternative that is maximally simple to use.

> Note
of course, experienced Perl hackers may find Listing 22.2 a bit longer than necessary when nearly the same changes can be accomplished from the command line like this:
# perl -p i.tap -e s/ beforestr/afterstr/g file(s)
See Chapter 25 for more information.

# WWW Retrieval

A question that arises frequently is to automate retrieval of pages from the World Wide Web. This section shows the simplest of many techniques.

# FTP Retrieval

Create a shell script, retrieve_one, with the contents of Listing 22.3 and with execution enabled (that is, type chmod +x retrieve_one).
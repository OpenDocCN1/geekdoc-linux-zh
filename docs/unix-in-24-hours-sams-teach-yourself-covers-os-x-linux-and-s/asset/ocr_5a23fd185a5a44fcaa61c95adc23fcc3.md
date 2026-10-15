```
iamcalled="browse.cgi"
webroot="/web"

echo "Content-type: text/html"
echo ""

echo "<h2>Directory $directory</h2><ul>"

cd $webroot/$directory

for filename in *
do
  case $filename in
    *.gif ) echo "<li><img src=$directory/$filename />"
            echo "<br /><tt>$filename</tt></li>" ;;
    *.jpg ) echo "<li><img src=$directory/$filename />"
            echo "<br /><tt>$filename</tt></li>" ;;
    *.htm ) echo "<li><a href=$filename>$filename</a></li>" ;;
    *.html ) echo "<li><a href=$filename>$filename</a></li>" ;;
    *)      if [ -d $filename ] ; then
              echo "<li><tt><a"
              echo "href=$iamcalled?$directory/$filename>"
              echo "[$filename]</a></tt></li>"
            else
              echo "<li><tt>$filename</tt></li>"
            fi
            ;;
  esac
done

echo "</ul>"

exit 0
```

This works well, but there’s much duplication of individual lines in the script, so this is a perfect case for a function. The first one I’ll define is showname:

Click here to view code image

```
function showname
{
  echo "<tt><b>$1</b></tt></li>"
}
```

This is simple enough, and now I have the statement in one spot, rather than three, making it easier to maintain and expand the script.

4. One more refinement: Case conditionals can have multiple expressions if they’re separated by the | or notation, which can make this considerably simpler:

Click here to view code image

```
#!/usr/local/bin/bash
# A Web-friendly directory browser that knows
# how to show graphic images:

directory=${QUERY_STRING:-$HOME}
iamcalled="browse.cgi"
webroot="/web"

function showname
{
  echo "<tt><b>$1</b></tt></li>"
```
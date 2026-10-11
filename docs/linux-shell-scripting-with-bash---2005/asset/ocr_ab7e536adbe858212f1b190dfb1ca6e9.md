```
print `"Content-type: text/html\r\n"

print "\r\n"



# Write HTML Header


print "<html>"

print "<head>"

print "<title>SSCRIPT results</title>"

print "</head>"

print "<body>"

print "<h1>SSCRIPT results</h1>"


# For POST, read the data into QUERY_STRING
# Otherwise, variables are already in QUERY_STRING

if [ "$REQUEST_METHOD" = "POST" ]; then
while read LINE; do
QUERY_STRING="$QUERY_STRING"$LINE"
done
QUERY_STRING="$QUERY_STRING"$LINE"
fi

# Generate Web Page to Return

# Display original, encoded variables

echo "Processing: $QUERY_STRING<br />"
```

```
print "<pre>"

decode "$QUERY_STRING" 2> "$ERRORS"

print "</pre>"


# Display any errors

if test -s "$ERRORS"; then
print "$ERRORS"
print "<table border="1" summary="errorlist">"
print "<tr bgcolor="White"><td>"
print "<font color="black" size="3"><b>"
print "<p><b>Error(s)</b><br />"
print "<pre>"
cat "$ERRORS"
```
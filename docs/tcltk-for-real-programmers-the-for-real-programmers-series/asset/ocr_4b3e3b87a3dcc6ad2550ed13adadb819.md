# 13.3 TClX

# Example 13.3-1

# Example Script

```
#!/usr/local/bin/tcl
proc scanTreeForString {topDir pattern matchString \
    filesWithfilesWithout} {
    upvar $filesWith
    upvar $filesWithout
    set with ""

# Create a scan context for the files that will be scanned.

# set sc [scancontext create]

# Add an action to take when the pattern is recognized
# in a file. If the pattern is recognized, append the
# file name to the list of files containing the pattern
# and break out of the scanning loop. Without the "break",
# scanfile would process each occurrence of the text that
# matches the regular expression.

scammatch sc "$matchString" {
    lappend with [file tail $filename]
    break;
}

# Process all the files below $topDir that match the
# pattern

for_recursive_glob filename $topDir $pattern {
    set fl [open $filename RONLY]
    scanfile sc $fl
    close $fl
# If there were no lines match the $matchString,
# there will be no $filename in the list "with".
```
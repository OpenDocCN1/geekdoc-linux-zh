# Chapter 15. Tips and Techniques

# Example 15.1-2

# Example Script

```
proc processLineProcedure {line} {
    puts "Processing $line"
}
puts "There are $argc arguments to this script"
puts "The arguments are: $argv"
set fileName [index argv 0]
set infile [open $fileName "r"]
while (![eof $infile]) {
    set len [gets $infile]
    if ($len > 0) {
        processLineProcedure $line
    }
}
```

# Debugging Session

```
%> tclsh
% set argv [list badFileName -option value]
badFileName -option value
% set argc 3
% source e15_1_2.tcl
There are 3 arguments to this script
The arguments are: badFileName -option value
could't open "badFileName": no such file or directory
% set errorInfo
could't open "badFileName": no such file or directory
while executing
    "open $fileName "r"
    (file e15_1_2.tcl line 9)
    invoked from within
"source e15_1_2.tcl
% processLineProcedure "This is a first Line from a file"
Processing This is a first Line from a file
%
```
# Chapter 4. Tcl Code Examples

```
# Open the bookmark file, and read in the data
#
set bookmarkFile [open "$bookmarkName" "r"]
set bookmarks [read $bookmarkFile]
close $bookmarkFile
#
# print out the result.
#
puts "[findUrl $argv $bookmarks]"
```

# 4.4 Speed

The question that always arises is “How fast does it run?” This is usually followed by “Can you make it run faster?” The time command times the speed of other commands.

Syntax: time cmd ?iterations?

+   time Returns the number of microseconds per iteration of the command.

+   cmd The command to be timed. Put within curly braces if you don't want substitutions done twice.

+   ?iterations The number of times to evaluate the command is defined, the time command returns the average time for these iterations of the command.

The time command evaluates a Tcl command passed as the first argument. The cmd argument will go through the normal substitutions as when time evaluates it, so you probably want to put the cmd variable within curly braces.
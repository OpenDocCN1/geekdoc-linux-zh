+   - -fixed-strings (or -F)—Treats the pattern as a string, ignoring any special meaning to the characters

+   - -invert-match (or -v)—Selects lines that do not match the pattern

+   - -no-filename (or -h)—Hides the filenames with each match

+   - -line-number (or -n)—Shows the line number with results

+   - -line-regexp (or -x)—Matches only an entire line

+   - -mmap—Uses memory mapping to speed up search on a file that won't shrink while grep is running

+   - -no-messages (or -s)—Suppresses error messages about missing files

+   - -null (or -Z)—Separates items with null characters instead of a carriage return

+   - -quiet (or -q)—Searches only to the first match and doesn't display it

+   - -regexp=P (or -E P)—Use string P as the matching pattern, useful for patterns starting with a period

+   - -with-filename (or -H)—Prints the filename with each match

+   - -word-regexp (or -w)—Only matches whole “words” separated from the rest of the line by spaces or other non-word characters

# find Command Switches

There are a large number of find expression switches. They include the following:

+   - -empty—Matches an empty regular file or directory

+   - -false—Always fails to match

+   - -fstype FS—The file must be on a file system of type FS

+   - -gid N—Matches numeric group ID N

+   - -group N—The file must be owned by this group ID. The group ID can be a name or number

+   - -daystart—Measures times from the start of the day rather than 24 hours ago

+   - -depth—Find the contents of a directory before the directory itself (a depth-first traversal)

+   - -file FILE—Writes -ls results to specified file

+   - -follow—Follows symbolic links. Normally, links are not followed

+   - -fprint F—Writes -print results to file F

+   - -fprint0 F—Writes -print0 results to file F

+   - -fprintf F FORMAT—Writes -printf results to file F

+   - -mindepth N—Descends at least N directories from the current directory

+   - -ilname pattern—Case-insensitive -lname
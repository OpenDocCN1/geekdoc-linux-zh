# find

find [path] [expression]

The find command is discussed in detail later in this chapter.

# grep

grep [options] string targetfile(s) command searches for a specified string in the

target file or the stdin stream (get regular-expression pattern) searches for matches if no filenames are given. grep is used often in a piped command to filter data before passing it or in scripts. A list of characters enclosed in [] brackets as the string argument matches any of the characters in the list. For example, the string [Hh][el]llo [Oo]o matches Hello or hello. The string [A-Za-z] matches any letter in either lowercase or capital form. The string [0-9] represents one-digit number. The caret ^ indicates the beginning of a line, and the dollar sign $ indicates the end of a line. The use of the string ^[A-Z] would match any line with a capital letter. Options include -i to ignore differences in case between the string and the input file line, -l to print the names of files containing matches, -r to attempt to match the string within all subdirectories as well, and -v to return all nonmatching lines.

# head

head [options] filename(s)

The head command prints by default the first ten lines of the specified file(s). The optional -n argument allows you to define how many lines, starting with line 1, will be printed.

# ispell

ispell filename

The ispell program checks the spelling of all words in the named file and prompts the user to accept the present spelling, replace it with a suggested spelling, add it to the dictionary, look up a specified string in the dictionary, change capital letters to lowercase, or quit the program. To learn about other more sophisticated uses see the man page.

# less

less [options] filename

The less command starts up a file viewer that allows up and down movement within the file being viewed. The less command doesn't require the entire file to be read before starting, so it tends to start up faster than commands that do. This is very frequently used on the command line as well as from another program.
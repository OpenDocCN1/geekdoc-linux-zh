File names can be entered in the File is named field, and a directory in which to start the search can be specified in the Look in folder field. In the example above, we search for the file *host s* in the `/etc` directory.

Wildcard searches are also possible using the expression syntax we used for *locate*. For instance, *host\** would search for all files starting with the characters *host* (and followed by one or more characters), and would therefore match *hosts*, *hosts.deny*, *hosts.accept*, and so on.

Clicking on the Additional Options label presents an advanced search interface using rules, as we described in Chapter 2.

# # Text Searches

Combining file searches with text searches within files allows us to quickly pinpoint the files that have the text we are looking for. We know how to search for a file by its filename (and also by its location); but how do we search the file system for files that contain a particular string of text? This type of search is very useful, but quite different from what we can achieve using *locate* or *find*.

The *grep* command is the most common way to search for a string in a file. In fact it can search multiple files at the same time. The *grep* command, by default, performs a case-sensitive search, though it can perform a case-insensitive search if required.

The *xargs* command reads its standard input and feeds it as arguments to any command that is supplied as an argument to it. In other words, *xargs* will dynamically create the arguments for a command. This makes it particularly useful for chaining commands using the pipe (\|) shell operator. As illustrated in Chapter 6, simply using a pipe operator feeds the output of a command as input to another command. The *xargs* command in conjunction with the pipe operator feeds the output of a command as arguments to another command. The following example illustrates its use.
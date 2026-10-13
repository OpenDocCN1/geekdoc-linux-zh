# Here Documents

An additional use of input redirection is in the creation of here documents. Say you need to send a list of phone numbers or URLs to the printer. You can enter the information that you want to send to the printer into the here document and then send that here document to the printer. This is much simpler than using a temporary file, which needs to be created and then should be deleted.

The general form for a here document is as follows:

```
cmd << delimiter
document
delimiter
```

Here the shell interprets the << operator as an instruction to read input until it finds a line containing the specified delimiter. All the input lines up to the line containing the delimiter are then fed into the standard input of the cmd. The delimiter tells the shell that the here document has been completed. Without it, the shell continues to read input forever. The delimiter must be a single word that does not contain spaces or tabs. For example, to print a quick list of URLs, you can use the following here document:

```
lpr << MYURLS
http://www.csua.berkeley.edu/~ranga/
http://www.cisco.com/
http://www.marathon.org/story/
http://www.gnu.org/
MYURLS
```

To strip the tabs in this example, you can give the << operator a - option.

You can also combine here documents with output redirection as follows:

```
cmd > file << delimiter
document
delimiter
```

If used in this form, the output of cmd is redirected to the specified file, and the input of cmd becomes the here document. For example, you can use the following command to create a file with the short list of URLs given previously:

```
cat > urls << MYURLS
http://www.csua.berkeley.edu/~ranga/
http://www.cisco.com/
http://www.marathon.org/story/
http://www.gnu.org/
MYURLS
```
tty Identify your workstation.

echo Hello, ello, llo, lo, o, o . . .  
Try typing echo "Hello world."

last Who last logged in and are they still logged in?

# Working with Files

Let me tell you the secret of computers, operating systems, and the whole industry that surrounds these things: Everything is data. Information is the be all and end all of everything we do with computers. Files are the storehouses for that information and learning how to manipulate them, use and abuse them, and otherwise play with them will still be the point of computers twenty years from now.

The next thing I want to talk about is the three most overlooked files on your system: standard in, standard out, and standard error. A facility in manipulating these "files" will provide you with amazing flexibility when it comes to doing your work.

# Commands to Know and Love, Part 2

ls LiSt files.

cat conCATenate files.  
cat /etc/profile  
sort SORT the contents of a file (or any output for that matter).  
sort /etc/passwd  
uniq Return only the UNIQue lines-you do this after sorting.  
wc Word Count (returns a count of words, characters, and lines).  
wc /etc/passwd  
cp CoPy files.  
mv MoVe, or rename, a file.  
rm ReMove, or delete, a file.  
more Allows easy paging of large text files.  
less Like the more command, but with serious attitude.
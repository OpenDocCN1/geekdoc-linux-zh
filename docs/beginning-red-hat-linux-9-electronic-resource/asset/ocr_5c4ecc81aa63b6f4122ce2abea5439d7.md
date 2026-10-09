```
grep farfalla file1 file2 ... filen
```

Here, file1, file2, ..., filen are the results of the search by the find utility.

# Other Text Searching Tools – awk and sed

There are other, more sophisticated text searching tools in existence. For example, the awk command is considered to be a language in itself, and allows for rich expressions and control flow. Another command, sed (the stream editor), is intended to transform input text streams, typically files or the output of commands.

The following awk script prints the login names and the actual names of users on the local system:

```
$ awk -F: '{print $1, "-", $5}' /etc/passwd
root - root
bin - bin
daemon - daemon
ftp - FTP User
nobody - Nobody
rpc - Portmapper RPC user
vcsa - virtual console memory owner
nscd - NSCD Daemon
sshd - Privilège-separated SSH
nfsnobody - Anonymous NFS User
xfs - X Font Server
ident - pident user
apache - Apache
webalizer - Webalizer
deepak - Deepak Thomas
```

The -F option here indicates the field separator. In this case, it is the colon (:) character that is used to separate fields in the /etc/passwd file. The awk action prints the first and fifth columns of the file to the standard output (that is, the terminal), with a hyphen (-) character separating column entries on each line.

The following sed command line transforms a string in the seashells.txt file. The expression 's/sells/shells;’ indicates that the pattern sells should be substituted with the pattern shells (the letter s indicates substitution):

```
$ cat >seashells.txt
She sells sea shells on the sea shore
^D
$ sed -e 's/sells;shells;’ seashells.txt
She shells sea shells on the sea shore
```

The commands awk and sed do not modify the input file directly. Instead, they treat the file as a stream of input and write the output to the standard output (in this case, the terminal).
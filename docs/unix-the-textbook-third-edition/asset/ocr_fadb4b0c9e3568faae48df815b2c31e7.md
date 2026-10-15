Art Pohn ... DIRECTORY
...
Done

We can illustrate the use of the here document feature with a simple instance of redirecting stdin of the cat command from the here document. The script in the heredoc_demo file is used to display a message for the user and then send a message to the person whose e-mail address is passed as a command line argument. In the following session, we use two here documents: one begins with << DataTag and ends with DataTag; and the other begins with << WRAPPER and ends with WRAPPER.

```
$ cat heredoc_demo
#!/bin/sh
cat << DataTag
This is a simple use of the here document. This data is the
input to the cat command.
DataTag

# Second example
mail -s "Weekly Meeting Reminder" $1 << WRAPPER
Hello,

This is a reminder for the weekly faculty meeting tomorrow.

Mansoor
WRAPPER
echo "Sending mail to $1 ... done."
exit 0
$ ./heredoc_demo eecsfaculty
This is a simple use of the here document. These data are the
input to the cat command.
Sending mail to eecsfaculty ... done.
$
```

The following script is more useful and makes a better utilization of the here document feature. The dext (directory expert) script maintains a directory of names, phone numbers, and e-mail addresses. The script is run with a name as a command line argument and uses the grep command to display the directory entry corresponding to the name. The -i option is used with the grep command in order to ignore the case of letters.

```
$ more dext
#!/bin/sh
if [ $# = 0 ]
then
echo "Usage: $0 name"
exit 1
```
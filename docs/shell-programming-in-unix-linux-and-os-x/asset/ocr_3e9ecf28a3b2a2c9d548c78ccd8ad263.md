# The && and || Constructs
161

If the conditional test is valid, nothing is done. If it's not valid, the error message is issued and
t program exited.

To be fair, this particular example could be reversed by restructuring the grep statement
(remember the 'i' argument to test?) sometimes it's easier to test for a positive condition
and doing nothing. In either case, this is where a well placed comment can
wonders when the code is read weeks or months later.

# The && and || Constructs

The shell has two special constructs that enable you to execute a command based on whether
t preceding command succeeds or fails. In case you think this sounds similar to the if
command, well it is. Sort of. It's a shorthand form of the if.

If you write
command, && command;

anywhere the shell expects to see a command, command, will be executed, and if it returns
an exit status of zero (success), command, will be executed. If command, returns a non-zero exit
status (fail), command, is not invoked if ordered.

For example you write
sort bigdata > /tmp/sortout && mv /tmp/sortout bigdata

then the mv command will be executed only if the sort is successful. Note that this is
equ to writing
sort bigdata > /tmp/sortout
then
mv /tmp/sortout bigdata

The command
[ -z "$EDITOR" && EDITOR=/bin/ed

tests the value of the variable EDITOR. If it's null, /bin/ed is assigned to it.
The construct works similarly, except that the second command gets executed only if the
ext status of the first is nonzero. So if you write
grep "$name" phonebook || echo "Couldn't find $name in
phonebook, or if it can't open the file phonebook). In this case, the equivalent if command
would like

if grep "$name" phonebook
then
:
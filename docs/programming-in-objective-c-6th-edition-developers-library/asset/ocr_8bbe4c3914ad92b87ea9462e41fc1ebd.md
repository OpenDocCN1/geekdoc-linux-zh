Seeds the random number generator to the u

value *seed*.

**i** **s)**

Gives the command contained in the character array pointed to by *s* to the system for execution, returning a system-defined value. If *s* is the null pointer, *s* returns a nonzero value if a command processor is available to execute your commands.

As an example, under Unix, the call

Click here to view code image

*s*

causes the system to create a directory called /* (assuming you have the proper permissions to do so).
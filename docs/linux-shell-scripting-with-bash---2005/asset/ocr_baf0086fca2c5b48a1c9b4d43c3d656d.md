# Listing 14.2	common.sh

```
```
# common.sh

# This script contains fragment global definitions and should be executed
# with the source command ( . ).

# Common constants

declare -rx SCRIPT=$0(#*/)              
declare -r ORDERS_DIR="/usr/local/orders"
declare -r ARCHIVE_DIR="$ORDERS_DIR/archive"
declare -r START_DATE="date"
```
```

Parameters in script fragments refer to the parameters included in the source command, not the original script. If there are no parameters included with source, the original script parameters are used.

You can end source script fragments prematurely with the return command. This command has the same format as the exit command. If you use exit, the entire script stops.

Because source script fragments aren't executed like a program, they do not need to have execute permissions to run; they simply need read permissions so that Bash can load them.

# Switching Scripts with exec

A third way to run a script is with the built-in exec command. When running another script or inserting a script fragment with source, control always resumes at the next line in the original script. The exec command instead provides an unconditional change to a new script. Bash discards the original script entirely, never to return. See Listings 14.3 and 14.4.

# Listing 14.3	exec1.sh

```
```
#!/bin/bash

# exec1.sh
#
# Source command example
shopt -s -o nounset

declare -rx SCRIPT=$0(#*/)
declare -r exec2="./exec2.sh"
if test ! -x "$exec2" ; then
	printf "\$SCRIPT:$LINENO: the script $exec2 is not available\n" >&2
	exit 192
```
```
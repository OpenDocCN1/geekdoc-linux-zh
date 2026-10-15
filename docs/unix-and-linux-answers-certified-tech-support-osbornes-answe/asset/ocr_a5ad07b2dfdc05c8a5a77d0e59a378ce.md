you move backward as well as forward. Pressing ^ while in pg places you in reverse search mode. Pressing / returns you to forward search mode.

# OPTIONS AND VARIABLES

+   - `-e` No pause at the end of a file.
+   - `-f` Don't split long lines.
+   - `-n` Issues a pg command without waiting for a carriage return.
+   - `-s` Messages and prompts display in standout mode (reverse video).
+   - `+number` Begin display at line number.
+   - `+/pattern` Start display at the first line containing pattern.
+   - `files` A list of space-delimited filenames.

# ping [options] host

# OBJECTIVE:

Tells you if another machine on the network is operational. This command sends out an ECHO_REQUEST packet to the specified machine. If the packet is sent and received successfully, the connection is considered alive.

# OPTIONS AND VARIABLES

+   - `-n` Displays network addresses as numbers.
+   - `-c count` Stop after sending count ECHO_RESPONSE packets.
+   - `-r` Bypass the normal routing tables and send directly to a host on an attached network.

# pr [options] files

# OBJECTIVE:

Lets you format a file while printing it to the standard output.

# OPTIONS AND VARIABLES

+   - `+page` Begins printing at the page number page.
+   - `-col` Specifies col columns of output.
+   - `-a` Prints files in a multicolumn format.
+   - `-d` Double-spaces the output.
+   - `-f` Separates the pages with a single form-feed command.
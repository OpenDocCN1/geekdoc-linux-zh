# 1396

# telnet

autoflush
If autoflush and localchars are both true, then when
a, intr, or quit characters are recognized (and
tformed into TELNET sequences; see set for
details), refuse to display any data on your terminal
until the remote system acknowledges (using a
NET Timing Mark option) that it has processed\hose TELNET sequences. The initial value for
toggle is true if you have not done a stty noflsh.
Otherwise, the value is false (see stty(1)).

autosynch
If asynch and localchars are both true, then when
type either the interrupt or quit characters (see
set for descriptions of interrupt and quit), send the
resulting TELNET sequence followed by the SYNCH
sequence. This procedure should throw away all
viously typed input on the remote system until both
of the TELNET sequences have been read and acted on.
The initial value is false.

binary
Enable or disable the BINARY option on both input and
output.

crlf
Determine how Returns are sent. If the value is true,
send Returns as CRLF. If the value is false, then
send Returns as CRull. The initial value is false.

cmod\Toggle Return mode. When this is enabled, most
Return characters received from the remote host. This mode\mapped into a Return followed by a linefeed. This mode\does not affect those characters you type, only those
received from the remote host. This mode is useful only
or remote hosts that send Return but never send a
linefeed. The initial value is false.

debug\Toggle socket-level debugging (only available to the
superuser). The initial value is false.

inbinary
Enable or disable the BINARY option on input.

localchars
If true, then recognize the flush, interrupt, quit,
erase, and kill characters (see set) locally
transform them into the appropriate TELNET sequence
se ac, ip, br, ek, and el (see send). The initial
value for this toggle is true in "old-line-by-line" mode
and false in "character-at-a-time" mode. When
LINEMODE option is enabled, ignore the value of
localchars and assume it is always true. If LINEMODE
has ever been enabled, then quit is sent as abort, and
eof and suspend are sent as e and susp (see send).

netdata
Toggle the display of all network data (in hexadecimal
format). The initial value is false.
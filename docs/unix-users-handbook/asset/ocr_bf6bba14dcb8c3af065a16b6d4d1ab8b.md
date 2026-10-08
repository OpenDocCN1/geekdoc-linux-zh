and kill characters (see set above) are recognized locally, and transformed into appropriate TELNET control sequences (respectively ao, ip, brk, ec, and el; see send above). The initial value for this toggle is TRUE in line-by-line mode, and FALSE in character-at-a-time mode.

**autoflush** If autoflush and localchars are both TRUE, whenever the ao, intr, or quit characters are recognized (and transformed into TELNET sequences - see set above for details), telnet refuses to display any data on the user's terminal until the remote system acknowledges (via a TELNET Timing Mark option) that it has processed those TELNET sequences. The initial value for this toggle is TRUE.

**autologin** Enable or disable automatic login into the Kerberos realm. Using this option yields the same results as using the -a option. The initial value for this toggle is TRUE.

**autosynch** If autosynch and localchars are both TRUE, when either the intr or quit character is typed (see set above for descriptions of the intr and quit characters), the resulting TELNET sequence sent is followed by the TELNET SYNCH sequence. This procedure should cause the remote system to begin discarding all previously typed input until both of the TELNET sequences have been read and acted upon. The initial value of this toggle is FALSE.

**binary** Enable or disable the TELNET BINARY option on both input and output. This option should be enabled in order to send and receive 8-bit characters to and from the TELNET server.

**crlf** If TRUE, end-of-line sequences are sent as an ASCII carriage-return and line-feed pair. If FALSE, end-of-line sequences are sent as an ASCII carriage-return and NUL character pair. The initial value for this toggle is FALSE.

**crmod** Toggle carriage return mode. When this mode is enabled, any carriage return characters received from the remote host are mapped into a carriage return and a line feed. This mode does not affect those characters typed by the user; only those received. This mode is only required for some hosts that require the client to do local echoing, but output "naked" carriage returns. The initial value for this toggle is FALSE.

**echo** Toggle local echo mode or remote echo mode. In local echo mode, user input is echoed to
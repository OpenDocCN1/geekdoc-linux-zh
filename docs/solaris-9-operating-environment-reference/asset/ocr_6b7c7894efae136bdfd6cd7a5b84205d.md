# 1394

# telnet

+   - flushoutput | Send an AO sequence to the remote host when in localchars mode and you type the flushout character. Take the initial value for the flush character to be the terminal flush character. 

+   - forwl | Forward partial lines to the remote system operating in LINEMODE (or "old-line-by-line" mode) and you type the forwl or for2 character. The initial values for the forwarding characters come from the terminal eol and eol2 characters.

+   - interrupt | Set the interrupt sequence that is sent to the remote host when in localchars mode (see toggle localchars) and you type the interrupt character. Take the initial value for the interrupt character to be the terminal intr character.

+   - kill | Send an EL sequence to the remote system when telnet is in localchars mode, operating in "character-at-a-time" mode, and you type the kill sequence. Take the initial value for the kill character to be the terminal kill character.

+   - lnext | Assume the lnext character is the terminal character when operating in LINEMODE or "old-line-by-line" mode. Take the initial value for the lnext character to be the terminal lnext character.

+   - quit | Send a BRK sequence to the remote host when in localchars mode and you type the quit character. Take the initial value for the quit character to be the terminal quit character.

+   - reprint | Assume the reprint character is the terminal reprint character when operating in LINEMODE or "old-line-by-line" mode. Take the initial value for reprint to be the terminal reprint character.

+   - rlogin | Set the rlogin escape character. Ignore the normal telnet escape character unless it is preceded by this character at the beginning of a line. Close the connection when the rlogin character followed by a is at the beginning of a line. When followed by a "Z", suspend the telnet command. The initial state is to disable the rlogin escape character.

+   - start | If the TOGGLE-FLOW-CONTROL option has been enabled, take the start character to be the terminal start character. Take the initial value for the kill character to be the terminal start character.
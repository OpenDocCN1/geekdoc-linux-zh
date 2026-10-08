processing), and suppressing echoing of entered characters (for entering, for example, a password).

escape This is the telnet escape character (initially ^\) which causes entry into telnet command mode (when connected to a remote system).

interrupt If telnet is in localchars mode (see toggle localchars below) and the interrupt character is typed, a TELNET IP sequence (see send ip above) is sent to the remote host. The initial value for the interrupt character is taken to be the terminal's intr character.

quit If telnet is in localchars mode (see toggle localchars below) and the quit character is typed, a TELNET BRK sequence (see send brk above) is sent to the remote host. The initial value for the quit character is taken to be the terminal's quit character.

flushoutput If telnet is in localchars mode (see toggle localchars below) and the flushoutput character is typed, a TELNET AO sequence (see send ao above) is sent to the remote host. The initial value for the flush character is ^O.

erase If telnet is in localchars mode (see toggle localchars below), and if telnet is operating in character-at-a-time mode, then when this character is typed, a TELNET EC sequence (see send ec above) is sent to the remote system. The initial value for the erase character is taken to be the terminal's erase character.

kill If telnet is in localchars mode (see toggle localchars below), and if telnet is operating in character-at-a-time mode, then when this character is typed, a TELNET EL sequence (see send el above) is sent to the remote system. The initial value for the kill character is taken to be the terminal's kill character.

eof If telnet is operating in line-by-line mode, entering this character as the first character on a line causes this character to be sent to the remote system. The initial value of the eof character is taken to be the terminal's eof character.

toggle arguments ... Toggle (between TRUE and FALSE) various flags that control how telnet responds to events. More than one argument can be specified. The state of these flags can be shown by using the display command. Valid arguments are:

+   localchars
If TRUE, the flush, interrupt, quit, erase,
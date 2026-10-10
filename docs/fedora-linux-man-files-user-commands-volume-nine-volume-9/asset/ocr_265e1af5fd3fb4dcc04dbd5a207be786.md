# › BUGS

Calling rz from most versions of (1) doesn’t work because cu’s receive process fights rz for characters from the modem.

Programs that do not properly implement the specified file transfer protocol may cause sz to “hang” the port for a minute or two. Every reported instance of this problem has been corrected by using ZCOMM, Pro-YAM, or other program with a correct implementation of the specified protocol.

Many programs claiming to support YMODEM only support XMODEM with 1k blocks, and they often don’t get that quite right.

Pathnas are restricted to 127 characters. In XMODEM single file mode, the pathna given on the command line is still processed as described above. The ASCII option’s CR/LF to NL translation rely deletes CR’s; undos(on) performs a more intelligent translation.
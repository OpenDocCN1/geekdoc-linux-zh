The terminal-information structure (`termios`) contains about 50 flag bits that tell the driver how to process characters coming in and going out, how to set communication-line parameters, such as the baud rate, and so on. The structure also defines several control characters, such as erase (normally Del or back-space), kill (normally Ctrl-u), and EOF (normally Ctrl-d).

Before you can change attributes, you need to call `tcgetattr` to initialize the structure. It’s complicated and possibly loaded with implementation-defined flags, so it’s impractical to just initialize a structure from scratch. After you get the structure, you adjust the flags and other fields as you like and then call `tcsetattr` to effect the changes. Its second argument, `action`, controls how and when the changes occur; one of these symbols is used:

+   **TCSDRAIN** Similar to `TCSANOW`, but wait for all pending output characters to be sent first. This should be used when output-affecting changes are made, to ensure characters previously output are processed under the rules in effect when they were written.

+   **TCSAFLUSH** Similar to `TCSDRAIN` but in addition to waiting for pending output to be drained, the input queue is flushed (characters are discarded). When beginning a new interactive mode, as when starting a screen editor, this is the safest command to use because it prevents characters that may have been typed ahead from causing an unintended action.

+   **TCANOW** Set the terminal immediately, according to the information in the structure.

The following subsections describe most of the commonly used flags and how they’re generally combined for typical uses (e.g., “raw” mode). For a complete list of standardized flags, see [SUS2002]. Or, you can execute `man termios` or `man termino` to see your implementation’s flags.

# 4.5.2 Character Size and Parity

Flags in `c_cflag` represent the character size (`CS7` for 7 bits; `CS8` for 8), the number of stop bits (`CSTOPB` for 2, clear for 1), whether parity should be checked (`PARENB` if so), and the parity (`PARODD` for odd, clear for even). There’s
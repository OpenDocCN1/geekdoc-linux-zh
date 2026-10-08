# 1372

# talk

# talk — Talk to Another User

# Synopsis

```
/usr/bin/talk address [terminal]
```

# Description

The talk command is a two-way, screen-oriented similar communication program.
When you first invoke it, talk sends a message similar to the following to the specified address.

```
Message from TalkDaemon@her-system at time...
talk: connection requested by your-address
talk: respond your-address
```

At this point, the recipient of the message can reply by typing:
talk your-address

Once communication is established, the two parties can talk simultaneously with their output displayed in separate regions of the screen. Characters are processed as follows.

+   * The alert character alerts the recipient's terminal.
* Control-L refreshes the screen's regions.
* The erase and kill characters affect the sender's terminal in the manner described by the termios(3) interface.
* The interrupt or end-of-file characters terminate the local talk command. Once the talk session has been terminated on one side, the other side of the talk session is notified that the talk session has been terminated and is able to do nothing except.
* Typing characters from the print or space LC_CTYPE classifications sends those characters to the recipient's terminal.
* When and only the stty local mode is enabled, additional special control characters and multibyte or single-byte characters are processed as printable characters if their wide-character equivalents are printable.
* Typing nonprintable characters writes them to the recipient's terminal: control characters appear as a caret (^) followed by the appropriate ASCII character, and with the high-bit set apart in "meta" notation. For example, \003 is displayed as ^C and \372 as M-z.

You can grant or deny permission to be a recipient of a talk message with the msg(1) command. However, a user privilege can further constrain the accessibility of other user terminals. Certain commands, such as pr(1), disallow messages to prevent interference with their output. talk fails when the user lacks the appropriate privileges to perform the requested action.

Certain block-mode terminals do not have all the capabilities necessary to support the simultaneous exchange of messages required for talk. When this type of exchange cannot be supported on such terminals, the implementation may support an reduced levels of simultaneous interaction, or it may report an error describing the terminal-related deficiency.
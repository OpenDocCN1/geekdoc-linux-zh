
## Chapter 3. Introduction to the Tcl Language

- myport port Defines the port number for the server side to open. If this is not supplied, then a port is assigned at random from the available ports.

- async Causes the socket command to return immediately, whether the connection has been completed or not.

- host The host to open a connection to. May be a name or a numeric IP address.

- port The number of the port to open a connection to on the host machine.

### 3.4.5 Buffered I/O

By default, Tcl I/O is buffered, like the stream-based I/O in the C standard library calls. In many cases, this is the desired behavior. If this isn't what your project needs, you can modify the behavior of the channel or flush the buffer on demand.

The fconfigure command lets you define the behavior of a channel. You can modify several options, including whether the channel should be buffered and the size of the buffer to use. The fconfigure command allows you to configure more options than are discussed in this book. You should read the online documentation for more details.

```
Syntax: fconfigure channelId ?name? ?value?
```

```
fconfigure Configure the behavior of a channel.
```

```
channelId The channel to modify.
```

```
name The name of a configuration field, which includes:
```

- -blocking boolean If true (the default mode), a Tcl program will block on a gets or read until data is available. If set false, gets, read, puts, flush, and close commands will not block.

### 3.5 Bottom Line

- buffering newValue If newValue is set to full, the channel will use buffered I/O. If set to line, the buffer will be flushed whenever a full line is received. If set to none, the channel will flush whenever characters are received.

The configure command was added to Tcl in version 7.5. If you writing code for an earlier revision of Tcl, or if you want to control when the buffers are flushed, you can use the flush command. The flush command forces buffered data to be written immediately.

```
Syntax: flush channelId
flush Flush the output buffer of a buffered channel.
channelId The channel to flush.
```

At this point, you know enough Tcl to write useful programs. There are many Tcl commands that were not covered in this chapter, but you have enough background that you can find the commands you need in the Tcl Command Reference on the CD-ROM.

The next chapter will work through a few examples to show how these commands (and a few new ones) can be used.

- A Tcl command consists of
  1. A command name
  2. Optional subcommand, options, or arguments
  3. A command terminator (either a semicolon (-) or a newline)
- An option will always start with a "." It may proceed or follow the arguments (depending on the command) and may require an argument itself.
- Tcl is a position-based language rather than a keyword-based language.
- Words and symbols must be separated by at least one whitespace character.

- - Multiple words or variables can be grouped into a single argument with braces ({}) or quotes ("").

- - Values are assigned to a variable with the set command.
`Syntax: set varName value`

- - Math operations are performed with the expr and incr commands.
`Syntax: expr mathExpression`
`Syntax: incr varName ?incrValue`

- - The branch commands are if and switch.
`Syntax: if {test} {bodyTrue} else {bodyFalse}`
`Syntax: switch ?option? string pattern1 body1\pattern2 body2? ?default?`

- - The looping commands are for, while, and foreach.
`Syntax: for start test next body`
`Syntax: while test body`

- - The list operations include list, split, length, lindex, and append.
`Syntax: list element1 ?element2? ... ?elementN?`
`Syntax: append listName ?element1? ... ?elementN?`
`Syntax: split data ?splitChar?`
`Syntax: length list`
`Syntax: lindex list index`

- - The string processing subcommands include first, match, toupper, tolower, and range.
`Syntax: string first substr string`
`Syntax: string match pattern string`
`Syntax: string tolower string`
`Syntax: string range string first last`

- - The array processing subcommands include names and get.

Syntax: array names arrayName ?pattern?

Syntax: array get arrayName

- - I/O is handled by the gets, read, and puts commands.

Syntax: gets channelID ?varName?

Syntax: read ?-newline channelID

Syntax: read channelID numBytes

Syntax: puts ?-newline ?channel outputString

- - Channels are created with the open and socket commands.

Syntax: open fileName ?access? ?permissions?

Syntax: socket ?options? host port

## Tcl Code Examples

This chapter will show how Tcl can be used. It will cover command evaluation and substitutions in a series of examples.

The first example in this chapter is a program to open a socket to a remote Post Office Protocol (POP) server and check for mail.

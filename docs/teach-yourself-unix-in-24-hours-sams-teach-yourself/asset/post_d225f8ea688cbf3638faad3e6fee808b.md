
# Glossary

**login shell** The shell you use, by default, when you log in to the system.

**login** A synonym for account name, this also can refer to the actual process of connecting to the UNIX system and entering your account name and password to your account.

**loop** This is a sequence of commands that are repeatedly executed while a condition is true.

**mail folder** A file containing one or more e-mail messages.

**mail header** The To;, From;, Subject;, and other lines at the very beginning of an e-mail message. All up to the first blank line are considered headers.

**mailbox** A synonym for mail folder.

**major number** For drivers, the major number identifies the specific type of device to use in the operating system. This is more easily remembered as the device ID number.

**man page** Each UNIX command comes with some basic online documentation that describes its function. This online documentation for a command is called a man page. Usually, the page lists the command-line flags and some error conditions.

**Meta key** Analogous to a Control key, this is labeled Meta or Alt on your keyboard.

**minor number** Once the driver is identified to the operating system by its major number, the address of the device in the computer itself (that is, which card slot a peripheral plugged into) is indicated by its minor number.

**modal** A modal program has multiple environments, or modes, that offer different capabilities. In a modal program, the Return key, for example, might do different things, depending on which mode you were in.

**mode** A shorthand way of saying permissions mode.

**modeless** A modeless program always interprets a key the same way, regardless of what the user is doing.

**multitasking** A multitasking computer is one that can actually run more than one program, or at a time. By contrast, most computers lock you into a single program that you must exit before you launch another.

**multiuser** Computers to handle more than a single person working on them simultaneously are designed to support multiple users, hence the term multiuser. By contrast, personal computers are almost always single-user because someone else can't be running a program or editing a file while you are using the computer for your own work.

**named emacs command** A command in emacs that requires you to type your name, like query-replace, rather than a command key or two.

**null character** Each character in UNIX has a specific value, and any character with a numeric value of zero is known as a null or null character.

**password entry** For each account on the UNIX system, there is an entry in the account database known as the *password file*. This also contains an encrypted copy of the password. This set of information for an individual account is known as the *password entry*.

**pathname** UNIX is split into a wide variety of directories and subdirectories, across often multiple hard disks and even multiple computers. So that the system needn't search laboriously through the entire mess each time you request a file, the set of directories you reference are stored as your search path, and the location of any specific command is known as its *pathname*.

**permission strings** The string that represents the access permissions.

**permissions mode** The set of accesses (read, write, execute) allowed for each of the three classes of users (owner, group, and everyone else) for each file or directory on the system. This is a synonym for access permission.

**pipeline** A series of UNIX commands changed by |, the pipe character.

**preference file** These are what files (hidden files) really are: they contain your individual preferences for many of the UNIX commands you use.

**preserve** Ensure that a message doesn't move out of your incoming mailbox even though you read it.

**print job name** The unique name assigned to a print job by the *lpr* or *lp* command.

**print queue** The queue, or list, in which all print jobs are placed for processing by the specific printer.

**process** A program stopped or running within the UNIX operating system. Also known as a job.

**recursive command** A command that repeatedly invokes itself.

**regular expressions** a convenient notation for specifying complex patterns. Notable special characters are ^ to match the beginning of the line and $ to match the end of the line.

**relative filename** Any filename that does not begin with a slash (/) is a filename whose meaning depends on where you are in the file system. For example, the file *test* might exist in both your home directory and in the root directory; */test* is an absolute filename and leaves no question which version is being used, but *test* could refer to either copy, depending on your current directory.

**replace mode** A mode of *vi* in which any characters you type replace those already in the file.

**Request for Comment** An official UNIX design specification, also known as an RFC.

**root directory** The directory at the very top of the file system hierarchy, also known as *slash*.

**row-first order** In contrast to column-first order, this is when items are sorted in rows so that the first item of each column in a row is in alphabetical order from left to right, the second line contains the next set of items, and so on.

**search path** A list of directories used to find a command. When a user enters a command, the shell looks in each directory in the search path to find a file, either until it is found or the list is exhausted.

**search string** The pattern specified in a search.

**shell** To interact with UNIX, you type in commands to the command-line interpreter, which is known as the *shell*, or *command shell*. the underlying environment in which you work with the UNIX system.

**shell alias** Most UNIX shells have a convenient way for you to create abbreviations for commonly used commands or series of commands, known as shell aliases. For example, if I always find typing `is -CF`, an alias can let you type `is` and the shell automatically adds the `-CF` flags each time.

**shell script** A collection of shell commands in a file.

**signals** Special messages that can be sent to stopped or running processes.

**slash** The root directory.

**standard error** This is the same as standard output, but you can re-direct standard error to a different location than standard output.

**standard input** UNIX programs always default to reading information from the user by reading the keyboard and watching what's typed. With redirection, input can come from a file, and pipelines, input can be the result of a previous UNIX command.

**standard output** When processing information, UNIX programs default to displaying the output on the screen itself, also known as standard output. With file redirection, output can be easily saved to a file; with pipelines, output can be sent to other programs.

**starting flag** Parameters that you specify on the command line when you invoke the program.

**stop a job** Run the program without terminating it.

**subshell** A shell other than the login shell.

**surfing** A style of interacting with the World Wide Web, usually for pleasure, where you follow hyperlinks from Web site to Web site.

**symbolic link** A file that contains a pointer to another file rather than contents of its own. This can also be a directory that points to another directory rather than having files of its own. A useful way to have multiple names for a single program or allow multiple people to share a single copy of a file.

**tilde command** A command beginning with ~ in Berkeley Mail or the Elm Mail System.

**transpose case** Switch uppercase to lowercase or lowercase to uppercase.

**undelete** Restore a deleted message to its original state.

**URL** The specification for a document on the World Wide Web. Usually, it includes a protocol, machine name, and filename.

**user environment** A set of values that describe the user's current location and modify the behavior of commands.

**user ID** A synonym for account name.

**variables** These are names to label data that may change during the execution of a program.

**wedged process** A process that is stuck in memory and can't free up its resources though it has ceased running. This is rare, but annoying.

**wildcards** Special characters that are interpreted by the UNIX shell or other programs to have meaning other than the letter itself. For example, * is a shell wildcard and creates a pattern that matches zero or more characters. Prefaced with a particular letter, X→X*—this pattern will match all files beginning with X.

**working directory** The directory where the user is working.

**World Wide Web** A collection of sites that provide hypertext documents on the Internet.

**XON/XOFF** A particular type of flow control. The receiving end can send an XON (delay transmission) character until it's ready for information, and when it sends an XOFF (resume transmission).

**zero-length variable** A variable that does not have a value assigned to it.

**zombie** A terminated process that has not been cleaned up by the parent process.

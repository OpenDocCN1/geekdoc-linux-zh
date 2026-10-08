The example in Listing 7-3 shows only memory information, but a variety of additional metrics are also available. Here is a summary of the information available for each process:

+   - User ID, PID, effective user ID, real and effective group ID, and parent PID
- Number of real pages used for data, text, or stack
- Number of real pages used for shared memory, memory mapped files, and so forth
- Number of virtual pages used for data, text, stack, shared memory, and so forth
- Priority and nice value
- Terminal device ID
- Process group and PRM group ID
- Address of process in memory
- User and system time spent executing
- Time process started
- Process status and status flags
- Processor last used by process
- Command line and executable base name for process
- CPU time used
- Current and high-water mark of resident set size
- Number of swaps, page faults, and page reclaims
- Number of signals or socket messages received
- Number of socket messages sent
- Scheduling policy of process
- Session ID
- File ID of process' root directory, current directory, and executable
- Highest file descriptor currently opened
- Number of characters read and written

More information about the process and system metrics available from this interface can be found in the system include file, /usr/include/sys/psstat.h.

# Fault Detection Tools

This section describes products that can be used to detect application failures. Additional tools for monitoring application performance are discussed later in the chapter.

# IT/Operations

IT/Operations (IT/O) is a sophisticated management product for system operators. Systems in the enterprise can be displayed on maps onscreen, with colors representing their current status. An Application Bank is included for default and customized tools that can be launched from a particular system. Events can be sent from systems throughout the enterprise, and configured recovery actions can then be taken.
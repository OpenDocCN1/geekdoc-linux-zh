# logger 709

command line, in which case each is logged immediately. If you specify command-line arguments, either the file indicated with -f or the standard input is added to the log. Otherwise, you can specify a file with a set of lines to be logged. If you specify no options, logger reads and logs messages on a line-by-line basis from the standard input.

# Options

+   - f file Use the contents of file as the message to log.
- i Log the process ID of the logger process with each line.
- p priority Log the message with the specified priority. The message priority can be specified numerically or as a facility.level pair. For example, -p local3.info assigns the message priority to the information level in the local3 facility. The default priority is user.notice.
- t tag Mark each line added to the log with the specified tag.

# Operands

+   - message One of the string whose contents are concatenated in the order specified, separated by single-space characters.

# Examples

The following example logs the message System rebooted to the default priority-level notice to be treated by syslogd in the same way as other messages to the facility user.
castle% logger System rebooted
caste%

The following example reads from the /dev/idmc and each line in file as a message with the tag HOSTID at priority-level notice to be treated by syslogd in the same way as other messages to the facility local0.
caste% logger -p local0.notice -t HOSTID -f /dev/idmc

# Environment Variables

See environ(5) for descriptions of the following environment variables that affect the execution of logger: LC_TYPE, LC_MESSAGES, and NLSPATH.

# Exit Status

+   - 0 Successful completion.
- >0 An error occurred.

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| Availability | SUNmcsu |
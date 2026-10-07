# The m4 Macro Language

The divert command directs the output stream to different targets. As of Sendmail 8.11, there are 11 different targets for the data stream. The 11 possible divert values are listed in Table 4.2.

# Table 4.2 Possible Values for the divert Command

| Value | Meaning |
| --- | --- |
| -1 | Discard output. |
| 0 | Send this data through normal processing. |
| 1 | Use this data for hostname resolution. |
| 2 | Add this data to ruleset 3. |
| 3 | Add this data to ruleset 0. |
| 4 | Add this data to the UUCP-specific sections of ruleset 0. |
| 5 | Use this data to define domain names this server will relay. |
| 6 | Add this data to the Local Info section of the sendmail.cf file. |
| 7 | Save this data as a mailier definition. |
| 8 | Use this data to define spammers blacklist. |
| 9 | Add this data to ruleset 1 or 2. |

Most of the values that can be specified with divert are used only by the Sendmail developers, who are in use, as buffers to hold data for specific parts of the sendmail.cf file. The data is collected in these buffers and then moved to the sendmail.cf file in the final stage of processing. It is possible to use any of these values in a configuration, but unlikely and unnecessary commands exist send data to the correct buffers without resorting to divert commands. For any reasonable configuration, the divert command is used with only two settings:

+   * divert is set to -1 to discard the output divert(-1) is found at the start of a block of text that is not written to the sendmail.cf file. While the block of text could be anything that's not intended for the output file, it is usually the copyright statement that is found at the beginning of many of the sample configuration files. The divert(-1) command at the start of the copyright means that the copyright is treated as a large comment.
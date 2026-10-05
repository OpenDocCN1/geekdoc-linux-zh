# A Quick Reference 365

# Table A.1 Sendmail m4 Macros and Configuration Commands (continued)

| Command | Usage |
| --- | --- |
| VIRTUSER_DOMAIN | Defines a virtual domain that will be accepted for processing through the virtusertable. |
| VIRTUSER_DOMAIN_FILE | Identifies the file that lists virtual domains that will be accepted for processing through the virtusertable. |

The built-in m4 commands shown in Table A.1—those listed in lowercase characters—are divided between two commands used to control the flow of output and two commands used to set macros. The two commands that control the flow of output are dn1 and divert. The dn1 command is used at the end of a line to clean blank lines from the output or at the beginning of a line to indicate the line is a command. The divert(-1) command marks the start of a block of text and the end of the block. In addition to -1 and 0, the divert command accepts other numeric arguments: 1 to 9. (See Table 4.2 in Chapter 4, "Creating a Basic Sendmail Configuration.") These other values are used in the Sendmail m4 macros to send direct data to various parts of the sendmail.cf file. But you will not use these values directly in your own configuration.

A group of macros—examples of which are LOCAL_CONFIG, LOCAL_RULESET, and MAILER_DEFINITION—allows you to send data to various parts of the sendmail.cf file without using the divert values directly. Commands such as LOCAL_CONFIG and MAILER_DEFINITION mark the start of raw sendmail.cf code that should be included in some part of the output file. These commands make it possible for you to customize the sendmail.cf file in any way. See the "Local Code" section later in this appendix for a full list of these macros.

The two built-in m4 commands that set and undefine sets a variable to a value and undefine it to its default value. More configuration parameters can be controlled through the define command than any other; consequently, more of this appendix is dedicated to define variables

Several of the macros—almost half—do essentially the same thing as the define command: they set a variable to a value. MASQUERADE_AS, MASQUERADE_DOMAIN, and VIRTUSER_DOMAIN_FILE are all examples of commands used to set variables. All of these commands are covered later in this appendix.

Appendices
# ## Messages

This section explains the conventions used for the ESSL messages and lists all the ESSL messages. For a description of each of the four types of ESSL messages, see “Dealing with Errors” on page 171.

# ## Message Conventions

This section describes the message conventions for the ESSL product.

# ### About Upper- and Lowercase

The literals, such as, ‘N’, ‘T’, ‘U’, and so forth, appear in the messages in this book in uppercase; however, they may be specified in your ESSL calling sequence in either upper- or lowercase, for example, ‘n’, ‘t’, and ‘u’.

# ### Message Format

The ESSL messages are issued in your output in the following format:

```
```
   rtn-name : 2538-mmmn
   message-text
```
```

![](bbox=[0.26, 0.38, 0.45, 0.4])

The parts of the ESSL message are as follows:

*rtn-name* gives the name of the ESSL subroutine that encountered the error.

**2538** is the ESSL component identification number.

*mmn* indicates the type of ESSL error message:

+   *   20—Input-argument error message
+   *   21—Computational error message
+   *   22—Input-argument error message
+   *   24—Resource error message
+   *   26—Information and attention message
+   *   27—Miscellaneous error message

*nn* is the message identification number.

*message-text* describes the nature of the error. Where one of several possible message-texts can be issued for a particular ESSL error, they are listed in this book with an “or” between them. The possible unique parts are:

+   *   The argument number of each argument involved in the error is included in the message description as (ARG NO. _)
+   *   Additional information about the error is included in the message. The placement of this information is shown in the messages as (_)

# ## Input-Argument Error Messages(2001-2099)

**RTN_NAME : 2538-2001 The number of elements (ARG NO. _) in a vector must be greater than or equal to zero.

**RTN_NAME : 2538-2002 The stride (ARG NO. _) for a vector must be nonzero.

**RTN_NAME : 2538-2003 The number of rows (ARG NO. _) in a matrix must be greater than or equal to zero.

**RTN_NAME : 2538-2004 The number of columns (ARG NO. _) in a matrix must be greater than or equal to zero.
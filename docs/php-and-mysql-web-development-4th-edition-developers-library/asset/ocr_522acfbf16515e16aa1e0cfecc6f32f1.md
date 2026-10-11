that you can concentrate more on what you're really interested in—being able to access
the content of your databases.

# ## 7.4  Processing SQL Statements

The purpose of connecting to the server is to conduct a conversation with it while the
connection is open. This section shows how to communicate with the server to process
statements. Each statement you execute involves the following steps:

+   1. Construct the statement. The way you do this depends on the contents of the statement—in particular, whether it contains binary data.
+   
+   2. Issue the statement by sending it to the server. The server will execute the statement
+   and generate a result.
+   
+   3. Process the statement result. This depends on what type of statement you issued. For
+   example, a SELECT statement returns rows of data for you to process. An INSERT
+   statement does not.

The MySQL client library includes two sets of routines for statement execution. The
first set is based on sending each statement as a string to the server and retrieving the re-
sults with all columns returned in string format. The second set is based on a binary pro-
tocol that enables non-string data values to be sent and returned in native format without
conversion to and from string format.

This section discusses the original method for processing SQL statements. Section 7.9,
“Using Server-Side Prepared Statements,” covers the binary protocol.

One factor to consider in constructing statements is which function to use for sending
them to the server. The more general statement-issuing routine is *mysql_real_query*().
With this routine, you provide the statement as a counted string (a string plus a length).
You must keep track of the length of your statement string and pass that to *mysql_real_*
*query*(), along with the string itself. Because the statement is treated as a counted string
rather than as a null-terminated string, it may contain anything, including binary data or
null bytes.

The other statement-issuing function, *mysql_query*(), is more restrictive in what it
allows in the statement string but often is easier to use. Any statement passed to
*mysql_query*() should be a null-terminated string. This means the statement text cannot
contain null bytes because those would cause it to be interpreted erroneously as shorter
than it really is. Generally speaking, if your statement can contain arbitrary binary data, it
might contain null bytes, so you shouldn’t use *mysql_query*(). On the other hand, when
you are working with null-terminated strings, you have the luxury of constructing state-
ments using standard C library string functions that you’re probably already familiar with,
such as *strcpy*() and *sprintf*().

Another factor to consider in constructing statements is whether you need to perform
any character-escaping operations. This is necessary if you want to construct statements
using values that contain binary data or other troublesome characters, such as quotes or
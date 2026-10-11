![](bbox=[0.135, 0.09, 0.89, 0.135])

Figure 3.17: Output example for command find

# Explanation of standard streams

In a Linux system, when a command is executed, there are three streams associated: one for the data input, one for the data output, and one for diagnostic or error output. These streams are associated with one name and one integer associated, as shown in the following table:

| Integer | Name | Stream description |
| --- | --- | --- |
| 0 | stdin | Standard input stream, the application receives data using this stream. |
| 1 | stdout | Standard output stream, the data will show the information using it. |
| 2 | stderr | Standard error stream, diagnostic, or errors will show using it. |


Table 3.7: Streams information and integer associated

When a command requires the user to enter data, the application will use the stdin to read what the user will type to introduce the data requested. When the application returns information to the user, it will send it to the standard output (stdout), and if there is any error or diagnostic information to be shown, it will use the standard error (stderr). The following illustration shows the standard streams information:
Option Description
-1[#] Changes the page length of the output, where # is the number of lines per page.
-h[new header text] Allows you to change what is included in the header at the top of each page, where [new header text] replaces the file name in the default header contents.

# Using pr with Piping

When you format your output with the pr command, you can send the formatted output to a file to be printed using the redirection operators (>) and pipe. For example, pr-145 sales>sales.out creates the sales.out file, which is formatted and ready for printing. In addition, you can send the formatted file directly to the printer using the lpr command. For example, the pr-145 sales|lpr command sends the formatted sales file directly to the default printer.

# How to Print Files

# Procedure Reference: Print a File Without Text Formatting

To print a file without text formatting:

+   1. Change to the directory that contains the file you want to print.
2. Print the file using cat[file name]|lpr

# Procedure Reference: Print a File With Text Formatting

To print a file with text formatting:

+   1. Change to the directory that contains the file you want to print.
2. Enter pr[options]({file name})|more to view the file with text formatting.
3. Enter pr[options]({file name})|lpr to print the file with text formatting.
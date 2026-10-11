# ## EXERCISE 10
## Getting a Handle on Things

# ### Part 1

+   1. Create a filehandle for reading from the *datebook* file (on the CD); print to another filehandle the names of all those who have a salary greater than $50,000.
+   2. Ask the user to input data for a new entry in the *datebook* file. (The name, phone, address, and so on, will be stored in separate scalars.) Append the newline to the *datebook* file by using a user-defined filehandle.

# ### Part 2

This problem appeared on a Web site called *daniweb.com*. Can you solve it?

+   1. We need a Perl program that will check whether or not an IP address entered by a user is valid. The user is to enter the IP address as a command-line parameter. For example, the user could type at the prompt
+      ```
+      check_ip.pl 192.168.9.23
+      ```
+      and the script will attempt to validate the IP address 192.168.9.23.
+   2. The script must first check whether the user has input any data and if not, display an appropriate error message. A valid IP address must have:
+      a. Four octets, each separated by a dot.
+      b. Only numbers are allowed in each of the four octets (meaning, no alphabetic or punctuation characters are allowed within each octet).
+      c. The first octet values are between 1 and 255. The second, third, and fourth octet values are between 0 and 255. Only one IP Address is to be input and validated (meaning, there is no looping through several IP addresses).

# ### Part 3

+   1. Use a pipe to list all the files in your current directory, and print only those files that are readable text files. Use the *die* function to quit if the open fails. For UNIX users, the command is *ls*. For Windows use *dir /b*. (Hint: Don't forget to *chomp!*).
+   2. Rewrite the program to test whether any of the files listed have been modified in the last 12 hours. Print the names of those files.
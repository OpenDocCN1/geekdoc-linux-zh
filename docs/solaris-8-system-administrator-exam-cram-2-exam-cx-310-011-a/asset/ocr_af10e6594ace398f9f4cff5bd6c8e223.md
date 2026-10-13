# Question 3

Give the command (without command-line arguments) used to add read/write permission for user account fred to a file owned by user account george.

The correct answer is **setfacl**.

# Question 4

+   To restrict logging in directly as root to the system console, which file needs to be modified?
+   
+   - a. `/dev/console`
+   - b. `/etc/passwd`
+   - c. `/etc/default/login`
+   - d. `/etc/default/su`

Answer c is correct. To restrict root login to the system console, you must modify the /etc/default/login file. /dev/console is the pathname for the console. Therefore, answer a is incorrect. /etc/passwd is the password file. Therefore, answer b is incorrect. /etc/default/su is the file that controls the behavior of the **su** command. Therefore, answer d is incorrect.

# Question 5

Where are user account passwords stored?

The correct answer is /etc/shadow.

# Question 6

+   The file test currently has the access mode 644. Which of the following will add mandatory locking? (Select all that apply.)
+   
+   - a. `chmod 2664 test`
+   - b. `chmod 2674 test`
+   - c. `chmod g+s test`
+   - d. `chmod g-x test`
+   - e. `setfacl -s u::rw-,g::rw-,o::r-- test`
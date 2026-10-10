
## Summarize the structure of a SQL database.
Each SQL installation consists of a number of named databases, each of which in turn may contain multiple tables. Each table can be thought of as a two-dimensional array of data. Each row in a table describes some object or concept (inventory items, employees, movies in a personal DVD collection, and so on), and each column in a table holds data about these objects or concepts (model number, salary, or director, for example).

## Describe the commands used to enter data in a SQL database.
The INSERT command inserts a single entry into a database. It requires a table name and a set of values, as in `INSERT INTO movies VALUES('Brazil', 'Terry Gilliam', 1985);`. The UPDATE command can be used in a similar way to update an existing entry, but you must use SET to specify the column to set and WHERE to identify the row or rows to be modified.

## Explain the commands used to extract data from a SQL database.
The SELECT command retrieves data from a SQL database. It can be used with a variety of additional options, such as FROM, JOIN, and WHERE, to identify the table or tables from which data should be retrieved and to locate specific values of interest.

# Review Questions

- Where is the best location for the current directory indicator (.) to reside in root's PATH environment variable?
  - A. Before all other directories.
  - B. After all other directories.
  - C. Nowhere; it shouldn't be in root's path.
  - D. Wherever is convenient.

- You want to create a shortcut for the command `cd ~/papers/trade`. Which of the following lines, if entered in a **bash** startup script, will accomplish this goal?
  - A. `alias cdpt='cd ~/papers/trade'`
  - B. `export cdpt='cd ~/papers/trade'`
  - C. `cd ~/papers/trade`
  - D. `shortcut cdpt 'cd ~/papers/trade'`

- What is the purpose of the EDITOR environment variable?
  - A. Set to **Y** (the default), the shell environment permits editing of commands; set to **N**, such editing is disallowed.
  - B. Some, but not all, programs refer to EDITOR to determine what external editor to launch when they do so.
  - C. If you type **edit filename** at a command prompt, the program specified by EDITOR will be launched.
  - D. Set to **GUI**, programs call a GUI editor; set to **TEXT**, programs call a text-based editor.

- In what environment variable is the current working directory stored?
  - A. `PATH`
  - B. `CWD`
  - C. `PWD`
  - D. `PRESENT`

- Which of the following commands, if typed in a **bash** shell, will create an environment variable called **MYVAR** with the contents **mystuff** which will be accessible to subsequently-launched programs?
  - A. `export MYVAR='mystuff'`
  - B. `MYVAR='mystuff'`
  - C. `$MYVAR==mystuff`
  - D. `echo $MYVAR mystuff`

- 6. What file might a user modify to alter his or her own bash environment?
  - A. `~/.startup`
  - B. `/etc/bashrc`
  - C. `/home/.bashrc`
  - D. `~/.bashrc`

- 7. What commands might you use (along with appropriate options) to learn the value of a specific environment variable? (Select all that apply.)
  - A. `env`
  - B. `DISPLAY`
  - C. `export`
  - D. `echo`

- 8. After using a text editor to create a shell script, what step should you take before trying to use the script?
  - A. Set one or more executable bits using `chmod`.
  - B. Copy the script to the `/usr/bin/scripts` directory.
  - C. Compile the script by typing `bash scriptname`, where `scriptname` is the script's name.
  - D. Run a virus checker on the script to be sure it contains no viruses.

- 9. Describe the effect of the following short script, `cp1`, if it's called as `cp1 big.c big.cc`:
  ```bash
  #!/bin/sh
  cp $2 $1
  ```
  - A. It has the same effect as the `cp` command—copying the contents of `big.c` to `big.cc`.
  - B. It compiles the C program `big.c` and calls the result `big.cc`.
  - C. It copies the contents of `big.cc` to `big.c`, eliminating the old `big.c`.
  - D. It converts the C program `big.c` into a C++ program called `big.cc`.

- 10. What is the purpose of conditional expressions in shell scripts?
  - A. They prevent scripts from executing if license conditions aren't met.
  - B. They display information about the script's computer environment.
  - C. They enable the script to take different actions in response to variable data.
  - D. They enable scripts to learn in a manner reminiscent of Pavlovian conditioning.

- 11. Which of the following lines identify valid shell scripts on a normally configured system? (Select all that apply.)
  - A. `#!/bin/script`
  - B. `#!/bin/bash`
  - C. `#!/bin/tcsh`
  - D. `#!/bin/sh`

- 12. Which of the following is **not** a valid looping statement in **bash** shell scripting?
  - A. `for`
  - B. `while`
  - C. `goto`
  - D. `until`

- 13. Your SMTP e-mail server, `mail.luna.edu`, receives a message addressed to `postmaster@mail.luna.edu`. There is **no** `postmaster` account on this computer. Assuming the system is properly configured, how should the e-mail server respond?
  - A. Deliver the e-mail to another account, either locally or on another computer.
  - B. Bounce the message so that the recipient knows the account doesn't exist.
  - C. Hold the message in the local mail queue until the `postmaster` account is created.
  - D. Delete the message without bouncing it so as to reduce e-mail clutter.

- 14. Which of the following is **not** a popular SMTP server for Linux?
  - A. Postfix
  - B. Sendmail
  - C. Fetchmail
  - D. Exim

- 15. You see the following line in a script:
  `mail -s "Error" -c abort < /tmp/msg root`
  What is the effect of this line, if and when it executes?
  - A. An e-mail is sent to the user `Error`, the script is aborted using `root` privileges, and error messages are written to `/tmp/msg`.
  - B. An e-mail with the subject of `Error` and the contents from `/tmp/msg` is sent to the local users `root` and `abort`.
  - C. An e-mail with the subject of `Error` and the contents of `/tmp/msg` is sent to the local user `root`, and then the script is aborted.
  - D. An e-mail is sent with `Error` priority to the local user `root`, and the e-mail system is then shut down with error messages being stored in `/tmp/msg`.

- 16. Your Internet connection has gone down for several hours. What is true of e-mail sent by your users to off-site recipients via a properly configured local SMTP server?
  - A. The SMTP server will refuse to accept e-mail from local clients during the outage.
  - B. E-mail will be neither delayed nor lost.
  - C. All e-mail sent during the outage will be lost.
  - D. E-mail will be delayed by a few hours but not lost.

- 17. You examine your /etc/aliases file and find it contains the following line: `root: jody`. What can you conclude from this?
  - A. E-mail addressed to jody on this system will be sent to the local user root.
  - B. E-mail addressed to root on this system will be sent to the local user jody.
  - C. The local user jody has broken into the system and acquired root privileges.
  - D. The local user jody has permission to read e-mail directly from root's mail queue.

- 18. You’ve just installed MySQL and run it by typing `mysql`. How would you create a database called `fish` to store data on different varieties of fish?
  - A. Type `NEW DATABASE fish;` at the `mysql>` prompt.
  - B. Type `create database fish;` at the `mysql>` prompt.
  - C. Type `NEW DATABASE FISH;` at the `mysql>` prompt.
  - D. Type `DATABASE CREATE fish;` at the `mysql>` prompt.

- 19. Which of the following are true statements about SQL tables? (Select all that apply.)
  - A. Multiple tables may exist in a single SQL database.
  - B. Tables may be combined for cross-table searches using the `DROP` command.
  - C. Tables consist of rows, each of which holds attributes, and columns, each of which defines a specific database item.
  - D. Careful table design can reduce the amount of data entry and database storage size.

- 20. What is the effect of the following SQL command, assuming the various names and data exist?
  ```sql
  mysql> UPDATE stars SET magnitude=2.25 WHERE starname= 'Mintaka';
  ```
  - A. It returns database entries from the stars table for all stars with magnitude of 2.25 and starname of Mintaka.
  - B. It sets the value of the stars field in the magnitude set to Mintaka, using a precision of 2.25.
  - C. It sets the value of the magnitude field to 2.25 for any item in the stars table with the starname of Mintaka.
  - D. It combines the stars and magnitude=2.25 tables, returning all items for which starname is Mintaka.

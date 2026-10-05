
# Chapter 10

- 1. LibreOffice, like most word processors, uses a binary format that can't be properly parsed using ASCII or Unicode text editor. Thus nano won't be useful in examining such a document, making option D correct. The nano text editor can handle ASCII or Unicode format, the text files described in options A and C are incorrect. The other document types described in options B and E are all likely or certain to be stored in ASCII or Unicode format, making them incorrect choices.

- 2. B, E The F6 and Ctrl+W keystrokes both invoke the search function, so options B and E are correct. The F3 key writes the current buffer to disk, so option A is incorrect. It enables or disables smooth scrolling, so option C is incorrect. Ctrl+S keystroke is an obscure one; Ctrl+F moves forward one character, so option D is incorrect.

- 3. In the vi editor, dd is the command-mode command that deletes lines. Preceding this command by a number deletes that number of lines. Thus option A is correct. Although yy works similarly, it copies (yanks) text rather than deleting it, so option B is incorrect. Option C works in many text editors, but not in vi. Option D works in emacs and similar text editors (including pico and nano), but not in vi. Option E, or something similar, works in many GUI editors, but not in vi, so it is incorrect.

- 4. False Unicode provides support for all alphabets, including the huge logarithmic systems used in common East Asian languages.

- 5. False Support for underlining, italics, multiple fonts, and similar advanced formatting features is present in word processors, not plaintext editors—even GUI text editors lack such support.

- 6. True Due to its ease of use, nano is typically the best editor to learn first.

- 7. 128

- 8. Ctrl+\ and Esc+R

- 9. u

- 10. ZZ

# Chapter 11

- 1. A Scripts, like binary programs, normally have at least one executable set, although they can be run in certain ways without this feature, so option A is correct. There is no standard /usr/bin/scripts directory, and scripts can reside in any directory, so option B is incorrect. Scripts are interpreted programs, which means that they don't need to be compiled. Typing bash scriptname will run the script; option C is incorrect. Viruses are extremely rare in Linux, and because you created the script, the only ways in which it could contain a virus would be if your system was already infected or if you wrote it as a virus. Thus option D is incorrect. Most spellcheckers are intended for English or other human languages, they lack valid Bash commands such as asac. Furthermore, even if every keyword is specified correctly, the script could contain bugs. Thus option E is incorrect.

- 2. C cp command is the only one called in the script, and that command copies files. Because the script passes the arguments ($1 and $2) in reverse order, their effect is reversed—whereas cp copies its first argument to the second name, the cp script copies the second argument to the first name. Option C correctly describes this. Option A ignores the reversed order of the arguments, so this option is incorrect. The cp command has nothing to do with compiling or C++ programs, and neither does the script, making option B incorrect. Since cp is a simple file-copying command, it can't convert a C program into a C++ program, making option D incorrect. The script's first line is a valid shebang line, contrary to option E, so that option is incorrect.

- 3. Conditional expressions return a true or false response, enabling the script to execute one set of instructions or another or to continue a loop. Option C is another way of saying this, and so it is correct. Conditional expressions have nothing to do with license conditions (option A), displaying information on the environment (option B), Pavlovian conditioning (option D), or executing the script at certain times of day (option E). That said, conditional expressions could be used in the service of any of these goals, but that is not their purpose.

- 4. False The $0 variable holds the name of the script—myscript in this example. To access the first parameter passed to the script (laser txt), the script must use the $1 variable.

# Answers to Review Questions

32

- 5. **True** You can use for execute a loop a fixed number of times, whereas while and until execute a test condition is no longer met or is met, respectively.

- 6. **False** The effect of the specified script is to launch three instances of terminal sequentially; the second launches only after the first terminates, and the third launches only after the second terminates. To do as the question specifies, you should include a trailing ampersand (&) in at least the first two calls to terminal (as in terminal &); this causes them to run in the background, so that the script can continue to execute the remaining instances of terminal.

- 7. #!/bin/sh

- 8. echo

- 9. case

- 10. exit

# Chapter 12

- 1. A UID 0 is reserved for the system administrator's account, also known as root, so option A is correct. The first ordinary user account is not a system account, and its UID is normally 500 or 1000, depending on the distribution, so option B is incorrect. Because A is correct, C cannot be correct. The association of UID 0 for administrative tasks is basic in Linux, so you won't find variation on this score, making option D incorrect. Option E describes the nobody account, which does not have a UID of 0.

- 2. A, C, E The /etc/passwd file's fields specify the username, an encrypted password (or x to denote use of shadow passwords, which is more common), a UID number (option A), a default GID number, a comment field that normally holds the user's full name, the path to the account's home directory (option C), and the path to the account's default text-mode shell (option E). Option B is incorrect because /etc/passwd includes the user's default group, the user may belong to additional groups that are defined elsewhere. Option D is incorrect because the user's default desktop environment is defined in the user's home directory, not in /etc/password.

# Appendix A - Answers to Review Questions

- 3. A sudo command is the usual way to execute a single command as root, and option A gives the correct syntax to use it as the question specifies. There is no standard root command, option B is incorrect. The passwd command changes passwords, option C is incorrect. Although you can use su to execute a single command as root, you must use it with the -c option to do this, as in su -c "cat /etc/", option D is incorrect. Option E's is a fictitious command, so option D is incorrect.

- 4. False whoami command displays your username. The id command displays your username, your UID number, your primary group name, your primary GID number, and the group names and GID numbers of all your groups.

- 5. False The name for the group data file in Linux is /etc/group, not /etc/groups.

- 6. True Its possible to do more damage to a command than root as an ordinary user. Thus you should be extra cautious using root—run only trusted programs, double-check your commands for errors, and so on.
- /etc/passwd

- 7. w

- 8. w

- 9. system

- 10. nonrepudiation

# Chapter 13

- 1. C userdel command deletes an account, and the -r option causes it to delete the user's home directory and mail spool, thus satisfying the terms of the question. Option A deletes the account but leaves the user's home directory intact. Option B does the same; the -f option forces account deletion and file removal from some circumstances, but it's meaningful only when -r is also used. Option D's command will probably have no effect, since rm works on directories only in conjunction with -r, and /home/nemo is probably the user's home directory. Option E's rm deletes the user's home directory (assuming it's located in the conventional place, given the username), but it doesn't delete the user's account.

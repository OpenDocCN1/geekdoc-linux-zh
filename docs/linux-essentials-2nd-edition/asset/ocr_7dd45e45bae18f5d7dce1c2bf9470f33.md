# Answers to Review Questions

32

+   5. **True** You can use for execute a loop a fixed number of times, whereas while and until execute a test condition is no longer met or is met, respectively.

+   6. **False** The effect of the specified script is to launch three instances of terminal sequentially; the second launches only after the first terminates, and the third launches only after the second terminates. To do as the question specifies, you should include a trailing ampersand (&) in at least the first two calls to terminal (as in terminal &); this causes them to run in the background, so that the script can continue to execute the remaining instances of terminal.

+   7. #!/bin/sh

+   8. echo

+   9. case

+   10. exit

# Chapter 12

+   1. A UID 0 is reserved for the system administrator's account, also known as root, so option A is correct. The first ordinary user account is not a system account, and its UID is normally 500 or 1000, depending on the distribution, so option B is incorrect. Because A is correct, C cannot be correct. The association of UID 0 for administrative tasks is basic in Linux, so you won't find variation on this score, making option D incorrect. Option E describes the nobody account, which does not have a UID of 0.

+   2. A, C, E The /etc/passwd file's fields specify the username, an encrypted password (or x to denote use of shadow passwords, which is more common), a UID number (option A), a default GID number, a comment field that normally holds the user's full name, the path to the account's home directory (option C), and the path to the account's default text-mode shell (option E). Option B is incorrect because /etc/passwd includes the user's default group, the user may belong to additional groups that are defined elsewhere. Option D is incorrect because the user's default desktop environment is defined in the user's home directory, not in /etc/password.
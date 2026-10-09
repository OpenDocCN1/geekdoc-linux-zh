# ## PASSWORDS

According to the **System Administration, Networking, and Security (SANS) Institute**, default and weak passwords constitute one of the most common security vulnerabilities. Few things are more unpopular with users than restrictive password policies. Unfortunately, without rigorous controls, people will often use simple, easily guessable words that are no match for the power of password cracking programs.

What makes a good password? It must be easy to remember, but it should not be a word found in the dictionary or one based upon easy-to-discover personal data. Passwords should be changed frequently; but if users are forced to change their passwords too often, they will often resort to using weaker passwords, defeating the original security goal.

Some of these issues can be resolved only by having a well-publicized password policy and by educating the user community on the danger of weak passwords. Fortunately, ADX 5L provides a number of tools and facilities that help to address some of these problems and enforce your defined policies.

# ## /etc/passwd and /etc/security/passwd

All UNIX-based operating systems store information about user accounts in the file `/etc/passwd`. Each user account on a system is represented by one line in this file, with individual fields separated by colons. The fields represent

+   *   The username
+       *   The user's encrypted password
+       *   The user identification number (UID)
+       *   The user's primary group identification number (GID)
+       *   The user's full name
+       *   The user's home directory
+       *   The user's shell

Several of the fields may be blank, as seen in this excerpt from an `/etc/passwd` file:

```
```
root::!::0:0:::/bin/ksh
daemon::!:1::1::/etc
...
jdoe::!:210:1:John Doe:/home/jdoe:/usr/bin/ksh
jane::!:211:1:Jane Plain:/home/jane:/usr/bin/ksh
```
```

Astute readers will notice that the second field, which should contain the user’s encrypted password, contains either an asterisk or an exclamation point. The reason for this concerns the solution to one of the biggest problems with the UNIX password scheme.
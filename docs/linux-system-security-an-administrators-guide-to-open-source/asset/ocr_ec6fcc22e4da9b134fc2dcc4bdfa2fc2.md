account on a Linux system represents a potential vulnerability (see Chapter 1). Here are some tips for creating and maintaining user accounts with security in mind.

+   * Choose good passwords.
+   * Ensure that all user accounts either have passwords or are locked.
+   * Use password aging and the shadow file.
+   * Maintain restrictive file permissions.
+   * Use pluggable authentication modules (PAM—discussed in Chapter 5).
+   * Use xlock or xscreensaver.

Additional user and group security management practices include accounting (discussed in Chapter 7), logging (discussed in Chapter 8 and Chapter 17), and auditing (such as with tiger, discussed in Chapter 13).

# Good Passwords

Choosing good passwords is a double-edged sword. You want users to pick passwords that are difficult to guess, yet easy to remember. Difficult to guess means that the password should not be something associated with the user, such as names of siblings, children, dogs, car license plates, or something that the user enjoys doing. If this type of password is chosen, anyone who even casually knows the user may be able to guess the user's *password*.

Good password choices should also not include dictionary words. Programs such as Crack (detailed in Chapter 12) will easily guess dictionary words and passwords based on dictionary words. For example, using g1zm0s as a password is a poor choice because it is based on the dictionary word *gizmos*. Even more complex variations make poor choices. For instance, 1r8d00dZ is based upon *later dudes*.

One way to select a difficult-to-guess password is to remember a sentence, such as:

> *The two foxes jumped over the brown fence.*

From this sentence, there are a number of ways to derive passwords; we give two examples. The first, T2jotbf, comes simply by taking the first letter from each word, except for the word two, which is replaced with the number 2. The second, h2ouhrr, is obtained by taking the second letter of each word, except again for the word two. Use your imagination to come up with other more sophisticated schemes. The point of this discussion is to encourage choosing difficult-to-guess, but easy-to-remember passwords.

Another approach to selecting good user passwords is to assign them. You could write or use an existing password-generating program or manually select passwords, such as i%8TQ#1r. In this way, you, the administrator, have complete control over user passwords. Unfortunately, your user probably won't
# TIP

An ideal password is at least eight characters long (the longer the better, actually), and contains a mixture of capital and lowercase letters, numbers, and punctuation marks or meta-characters. To keep your system security strong, you must ensure that users follow these guidelines when picking a password with the passwd program in FreeBSD.

Although the only password security measure currently enforced by the default passwd program in FreeBSD is that passwords must be at least six characters long, the FreeBSD development community is working to incorporate further weak-password checks into the passwd program.

You learn how to set the login.conf program to set a minimum password length and to require periodic password updates in “Forcing Password Expiration,” later in this chapter.

# Enforcing Secure Passwords with Crack

The first priority in maintaining secure user password practices is to prevent users from choosing insecure passwords in the first place. As of this writing, the best way to make sure your users aren’t using easily guessable passwords is to periodically try to guess them yourself. A tool called Crack, available in the ports collection at /usr/ports/security/crack, helps you do just that. Although it may appear to be a “hacker” tool, Crack is primarily intended as a security-auditing tool for system administrators, allowing you to perform “dictionary” attacks (trying a plethora of English words as potential passwords) as well as a number of other commonly used “convenience” passwords: repeated strings, the user’s login name, groups of numbers, and so on. Crack helps you determine which of your users are using insecure passwords. You can then contact these users directly and ask them to adhere to the password rules you set.

You can build and install the Crack port using the instructions in Chapter 14, “Installing Additional Software.” The new /usr/local/crack directory’s permissions enable only root to list its contents or run any of its programs. To check your system’s user database for weak passwords, go into /usr/local/crack and run the Crack program like this (note the capitalization):

```
# . /Crack -fmt bsd /etc/master.passwd
```

The Crack program builds some utilities, compiles some dictionaries, and then launches its arsenal against /etc/master.passwd. Crack sends its output into runtime files that you can analyze with the Reporter program, as shown here:

```
# . /Reporter -quiet
---- passwords cracked as of Sun Jan 14 12:17:41 EST 2001 ----

97969312:Guessed frank [frank] Frank Jones [/etc/master.passwd /bin/tos h]
97969318:Guessed joe [password] Joe User [/etc/master.passwd ->/usr/local/bin/bash]

---- done ----
```
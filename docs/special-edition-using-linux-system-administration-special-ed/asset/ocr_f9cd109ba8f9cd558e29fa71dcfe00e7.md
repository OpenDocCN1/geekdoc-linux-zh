enter your password. Don’t enter your password into a computer you don’t trust. Use the password for a limited time and change it periodically.

# CHOOSE A HARD-TO-GUESS PASSWORD

passwd will try to prevent you from choosing a really bad password, but it isn’t foolproof; create your password wisely. Don’t use something you’d find in a dictionary (in any language or jargon). Don’t use a name (including that of a spouse, parent, child, pet, fantasy character, famous person, or location) or any variation of your personal or account name. Don’t use accessible personal information (such as your phone number, license plate, or social security number) or your environment. Don’t use a birthday or a simple pattern (such as backward, followed by a digit, or preceded by a digit. Instead, use a mixture of upper and lowercase letters, as well as digits or punctuation. When choosing a new password, make sure it is unrelated to any previous password. Use long passwords (say 8 characters long). You might use a word pair with punctuation inserted, a passphrase (an understandable sequence of words), or the first letter of each word in a passphrase.

These principles are partially enforced by the system. Vigilance on your part will make the system much more secure.

# EXIT CODE

On successful completion of its task, passwd will complete with exit code 0. An exit code of 1 indicates an error occurred. Textual errors are written to the standard error stream.

# CONFORMING TO

Linux-PAM (Pluggable Authentication modules for Linux). If your distribution of Linux-PAM conforms to the Linux File System Standard, you can find the modules in `/lib/security/` instead of `/usr/lib/security/`, as indicated in the example.

# FILES

`/etc/pam.d/passwd` - the Linux-PAM configuration file

# BUGS

None known.

# SEE ALSO

pam(8), and pam_chautok(2).

For more complete information on how to configure this application with Linux-PAM, see the Linux-PAM System Administrators’ Guide at

```
<http://parc.power.net/morgan/Linux-PAM/index.html>.
```
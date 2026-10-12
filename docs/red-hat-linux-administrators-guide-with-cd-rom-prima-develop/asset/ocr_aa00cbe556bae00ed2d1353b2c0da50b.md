crypt() function. Once a password has been hashed with MDS, you can no longer convert it back to a simple text file. This helps to prevent spying eyes from gaining easier access to the original file, but does not eliminate the possibility that the password could still be guessed using brute force cracking methods.

# NOTE

Shadow passwords originally began on such UNIX-based systems as Solaris, but they have since been adopted by nearly all Linux distributions, including Red Hat. On the latest Red Hat release you have the option to install shadow passwords and enable MDS hashing. These are selected by default and it is a wise decision to allow them to remain so.

Unique system users such as nobody and bin do not normally allow a password to be affixed to them. To ensure that these types of files are not misused, it is a good idea to verify that no password is kept in the field that normally stores the encrypted passwords. An asterisk, or star, should appear instead of the password. This ensures that no one can physically log in under that assumed username. The same can be done on a regular user. By replacing the gibberish of encrypted text with an asterisk, you ensure that the user is no longer validated to log on with a password.

Listing 5.1 shows sample output from an /etc/shadow file. Notice the difference between the users with UIDs under 500 and the five valid users—four normal users and root.

# Listing 5.1 A Selection Taken from a Sample /etc/shadow File

```
root:*$1$sYQciqsIZUxHm3xc3IRpMgUWr4YJmL E0:10873:0:99999::7:-1:134538460
bin::10819::99999::7::
daemon::10819::99999::7::
adm::10819::99999::7::
ip::10819::99999::7::
sync:10819::99999::7::
shutdown::10819::99999::7::
halt:*10819::99999::7::
mail::10819::99999::7::
news::10819::99999::7::
uucp::10819::99999::7::
```
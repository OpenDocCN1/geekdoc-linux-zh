networking protocols that do not play well with passwords longer than eight characters. For example, only the first eight characters are significant in NIS+ passwords because the underlying secure-RPC protocol uses DES.

Consider the following suggestions when choosing a password-hashing algorithm for your system:

+   - When using DES, set the minimum password length to be at least six; use an eight-character password for root.
+   - If all interconnected systems support MD5, use MD5 as the password-hashing algorithm and set the minimum password length to be at least six.
+   - Consider using Blowfish for all system accounts that require a password. (However, this means you need to switch the password-hashing method from the current setting to Blowfish, change the password, and restore the setting. An alternative is to install the Blowfish-aware version of Perl—the version included with SLES 9 supports only DES and MD5—so you can use a simple script to first generate the hashed value using Perl and then set the password using `usermod -p hashed_value`.)

# TIP

You can find the RPM for a version of Perl that supports Blowfish at http://rpmfind.net/linux/RPM/contrib/libc6/i386/perl-Crypt-Blowfish-2.09-1.i386.html and at http://rpmfind.net/linux/RPM/suse/8.2/i386/suse/i586/perl-Crypt-Blowfish-2.09-188.i586.html. The Perl crypt home page is at http://pan.cog.uk/modules/Crypt.

In most cases, MD5 provides the best balance between performance and security.

# Auditing Default Accounts

As mentioned earlier, a number of system accounts exist to allow programs to be run as the UID associated with that account; they are not direct login accounts. FTP, named (for DNS), mail, and news are some examples of such system accounts. Make sure such accounts are prevented from a terminal login by setting their shell to `/bin/false` or similar.

If the services for these accounts are not in use, uninstall them and remove the accounts—or at the very least, disable unused services (see Chapter 8 for more information). Periodically, you should check the contents of `/etc/passwd` and `/etc/shadow` to ensure that the removed system accounts didn’t “spontaneously
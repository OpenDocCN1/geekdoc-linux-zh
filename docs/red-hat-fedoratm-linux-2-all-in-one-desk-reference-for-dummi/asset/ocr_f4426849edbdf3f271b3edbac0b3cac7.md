In this case, note that the second field contains an x instead of an encrypted password. The x is the *shadow password*; the actual encrypted password is now stored in the `/etc/shadow` file where the entry for `root` looks like this:

```
root:$1$AAnI/yN$uEShbzUppY9c$foo1Bf0t$S0:11077:0:99999:7:-1:1:134540536
```

The format of the `/etc/shadow` entries with colon-separated fields resembles the entries in the `/etc/passwd` file, but the meanings of most of the fields differ. The first field is still the username, and the second one is the encrypted password.

The remaining fields in each `/etc/shadow` entry control when the password expires. You don't have to interpret or change these entries in the `/etc/shadow` file. Instead, use the `chage` command to change the password-expiration information. For starters, you can check a user's password-expiration information by using the `chage` command with the `-l` option, as follows (in this case, you have to be **logged in as root**):

```
chage -l root
```

This command displays expiration information, including how long the password lasts and how often you can change the password.

If you want to ensure that the user is forced to change a password every 90 days, you can use the `-M` option to set the maximum number of days that a password stays valid. For example, to make sure that user `naba` is prompted to change the password in 90 days, I log in as **root** and type the following command:

```
chage -M 90 naba
```

You can use the command for each user account to ensure that all passwords expire when appropriate, and that all users must pick new passwords.

# Pluggable authentication modules (PAMs)

In addition to improving the password file's security by using shadow passwords, Fedora Core also improves the actual encryption of the passwords stored in the `/etc/shadow` file, using the MD5 message-digest algorithm described in RFC 1321 (`www.ietf.org/rfc/rfc1321.txt` or `www.cis.ohio-state.edu/cgi-bin/rfc/rfc1321.html`). MD5 reduces a message of any length to a 128-bit message digest (or *fingerprint*) of a document so you can digitally sign it by encrypting it with your private key. MD5 works quite well for password encryption, too.

![](bbox=[0.87, 0.52, 0.99, 0.7])
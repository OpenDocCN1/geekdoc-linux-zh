You can find more information about Kerberos by looking at the Kerberos FAQ( http://www.cis.ohio-state.edu/hypertext/faq/usenet/kerberos-faq/general/faq.html), and the code can be found at http://nii.isi.edu/info/kerberos.

From: Stein, Jennifer G., Clifford Neuman, and Jeffrey L. Schiller. “Kerberos: An Authentication Service for Open Network Systems.” USENIX Conference Proceedings, Dallas, Texas, Winter 1998.

Kerberos should not be your first step in improving security of your host. It is quite involved, and not as widely used as, say, ssh.

# Shadow Passwords

Shadow passwords are a means of keeping your encrypted password information secret from normal users. Normally, these encrypted passwords are stored in /etc/passwd file for all to read. Anyone can then run password guesser programs on them and attempt to determine what they are. Shadow passwords, by contrast, are saved in /etc/Shadow, which only privileged users can read. In order to use shadow passwords, you need to make sure all your utilities that need access to password information are recompiled to support them. PAM (above) also allows you to just plug in a shadow module; it doesn't require recompilation of executables. You can refer to the Shadow-Password HOWTO for further information if necessary. It is available at http://metalab.unc.edu/LDP/HOWTO/Shadow-Passw0rd-HOWTO.html. It is rather dated now, and will not be required for distributions supporting PAM.

# Crack and John the Ripper

If for some reason your passwd program is not enforcing hard-to-guess passwords, you might want to run a password-cracking program and make sure your users' passwords are secure.

Password cracking programs work on a simple idea: they try every word in the dictionary, and then variations on those words, encrypting each one and checking it against your encrypted password. If they get a match they know what your password is.

There are a number of programs out there–the two most notable of which are Crack and John the Ripper ( http://www.fa1se.com/security/john/index.html). They will take up a lot of your cpu time, but you should be able to tell if an attacker could get in using them
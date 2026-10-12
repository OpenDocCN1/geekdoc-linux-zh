+   - lcredit=n—The maximum additional credits for having lowercase characters in the password at 1 credit per lowercase character. (Default = 1.)
+   - ocredit=n—The maximum additional credits for having other characters in the password at 1 credit per other character (!$% and so on. Default = 1.)

The following is an example for a pam_cracklib module line:

```
passwd password required pam_cracklib.so difok=5 minlen=16 dcredit=2 ocredit=2
```

Using cracklib properly will guarantee that your passwords are very difficult to guess, and it is recommended that you edit the pam_cracklib line in /etc/pam.d/passwd to force users to have reasonable passwords.

# Beware of Overly Strict Password Policies

Will having complex password rules help to lock down your system? So it would seem, but in fact, the security problem can move from your system to your users' workplaces, which are far more difficult to police. If the password rules are too strict and passwords become a meaningless jumble of letters and numbers, users are going to find it difficult to remember them, and instead will write them down. Now the password is committed to paper, which someone else can either read or steal. If you're lucky, the piece of paper will be kept in a safe place and not taped to the user's monitor, but I wouldn't count on it.

Although there is not much you can do to prevent users from writing down their passwords, you can at least make it possible for them to remember. Make the password rules loose enough so that the users can choose passwords that they can remember while still giving you the security you require on your system. Increasing the minimum length is a good start. If you are using MD5 (which is recommended), your password length is not limited to eight characters, and that allows your users to be a little less cryptic in choosing a password that satisfies your password rules. You may want to inform your users that they do not have to choose a pass-word, per se—spaces are allowed, so a pass-phrase is possible. A pass-phrase might be easier for your users to remember and will still provide you with the security you require. If you are going to encourage long passwords with a high minlength, make sure your difok is set accordingly. If someone enters a long password containing all the letters in the alphabet, it will be very difficult to choose a new password that has a sufficient number of different characters.
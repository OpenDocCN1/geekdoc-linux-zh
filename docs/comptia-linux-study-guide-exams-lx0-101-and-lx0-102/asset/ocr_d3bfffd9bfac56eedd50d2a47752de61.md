# Administering Local Security

489

Use Remote Login Protocols Certain remote login protocols are inherently insecure; all data traverse the network in an unencrypted form. Intervening computers can be configured to snatch passwords from such sessions. Because of this, it's best to disable Telnet, FTP, and other protocols that use cleartext passwords in favor of protocols that encrypt passwords, such as SSH.

Be Alert to Shoulder Surfing If your users log in using public terminals, as is common on college campuses, in Internet cafes, and the like, it will be others able to watch them type their passwords—a practice sometimes called shoulder surfing. Users should be alert to this and minimize such users log in.

Use Each Password on Just One System If one computer's password database is compromised and if of that users reuse passwords on other systems, then other systems can be compromised. For this, it's best to use each password just once. Unfortunately, the proliferation of Web sites that require passwords for access makes this rule impossible to enforce, without violating the rule of not writing the password.(Modern browsers can remember passwords for you, but this is by storing them in a file—essentially, writing them down). A reasonable compromise might be to use one password for the least-sensitive Web sites (such as online newspapers) and unique passwords for sensitive Web sites (such as banking sites) and login accounts.

Be Alert to Social Engineering Crackers often use social engineering to obtain passwords. This practice involves tricking individuals into giving up their passwords by pretending to be a system administrator or victims by misleading them. Amazing. A related practice is phishing, in which an attacker puts up a fake Web site or sends an email pretending to be someone else. The victim is lured into revealing sensitive data (such as credit card numbers).

Some of these steps are things you can do, such as replacing insecure login protocols with encrypted ones. Others are things your users must do. This illustrates the importance of user education, particularly on systems with many users.

# Choosing a Good Password

As a rule, people tend to be lazy when it comes to security. In computer terms, this means users tend to pick passwords that are easy to guess, and they change those passwords infrequently. Both conditions make a cracker's life easier, particularly if the cracker knows it. Fortunately, Linux includes tools to help your users select good passwords and change them regularly.

Poor but common passwords include those based on the following:

+   - The names of family members, friends, and pets
- Favorite books, movies, television shows, or the characters in any of them
- Telephone numbers, street addresses, or Social Security numbers
- Any other meaningful personal information
- Any single word that's found in a dictionary (in any language)
- Any simple keyboard or alphanumeric combination, such as qwerty or 123456
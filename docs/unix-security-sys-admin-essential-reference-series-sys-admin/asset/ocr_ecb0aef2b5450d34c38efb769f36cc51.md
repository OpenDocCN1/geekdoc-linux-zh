# Tip 9: Watch the Security Mailing Lists on the Internet

There are a number of security-related mailing lists available on the Internet. You should probably subscribe to a few of them to keep informed of the newest exploits and problems. In any case, it is a good idea to subscribe to the CERT mailing list. This is one of the official organs that releases security alerts and fixes. Visit their Web site at http://www.cert.org for more information on subscribing.

# Tip 10: Always Test a Password Scheme before Implementing It

In this picture of networking security, there is still one big unknown: the human factor. You can build a very safe networking environment, but if users stick their password on the monitor to remember it, you still have a major problem. This may sound crazy, but it actually happened when a security policy forced users to use system-generated passwords. These passwords were so difficult to remember that users wrote them on yellow notes and stuck them to their monitors or (if more security-aware) to the bottom of their keyboards.

You need to involve your users and make them security-aware so they are willing to cooperate. You will also need to draw up some guidelines for the users to follow so they can continue working in a safe manner.

With respect to the human factor, some companies enforce a password policy to prevent users from using guessable passwords. This is wise, but such a password scheme should be selected with care. In some cases, this scheme leads to a situation where passwords are generated automatically, which often results in passwords like Grb16x or Pfq#12. Admittedly, these passwords are hard to guess, but are probably even harder to remember. You might have users follow a rule similar to this: Make up a sentence of words and numbers you can easily remember. Pick all the first letters from each word and the numbers, and use these as your password. For example, "I live in Holland and my zipcode is 9991 AM" would translate to the password I1iHamy9A. This is also hard to guess, but at least it is easier to remember. (BTW, this is not my real password.)

You could also write a password program that will check the new password of a user against a (preferably large) dictionary before accepting it. Whenever the program finds a match with a word in the dictionary, the password is rejected, and the user must choose a new one.
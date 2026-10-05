
# Creating Users and Groups

Linux is a multiuser OS, meaning that a single Linux computer can support many users, each with a unique account. With this capability comes the need to manage users' accounts, and this chapter covers the procedures you'll use to do so.

The chapter begins with information on how to create accounts. With the accounts created, you then need to know how to modify those accounts and, when necessary, delete them. Finally, groups are similar to accounts in many ways, so how to create and manage groups is described.

- Creating new accounts
- Modifying accounts
- Deleting accounts
- Managing groups

# Creating New Accounts

In many environments, the task of adding accounts is quite common. Large businesses hire new employees, universities recruit new students, charitable organizations obtain fresh volunteers, and so on. Thus you must know how to create accounts. Before covering the mechanics of creating accounts, the important issues of deciding how to use groups and selecting a good password are described. How to create accounts using both GUI and text-mode tools are explained afterward.

# Deciding on a Group Strategy

As described in Chapter 12, “Understanding Basic Security,” Linux groups are collections of users. You can use groups to control who can access particular files. As will be described in Chapter 14, “Setting Ownership and Permissions,” individuals can change the group affiliations and group permissions of their own files. Thus the way that you use groups can influence your computer's overall security strategy. Two approaches are common:

**User Groups** Each user can have an associated group; for instance, the user can have a group ownership on his files to set group permissions to whatever is desired, and the system administrator can add users to the user group. Thereafter, members of the group may access files in this group by using the permissions determined by the user luke. This approach emphasizes controlling access to individual users' files.

**Project Groups** In this method, you create groups on work projects, departmental affiliations, or other real-world groupings of users. For instance, you might have a group called sales for the sales department. Members of this group who share files with other members of this group would assign group ownership and permissions appropriately and store files in an agreed-upon location. This approach works best when the computer is used by a large number of people who collaborate in easily defined groups.

By default, some distributions employ a group strategy and others use a project group strategy. In the latter case, most users are in a group called users or something similar by default.

These two approaches are not mutually exclusive; you can mix and match, or create your own approach. You should also realize that users can be members of multiple groups. In fact, this is required for the user groups to work at—otherwise, groups are redundant with accounts.

If you use the group approach, you should think about which group should be a new user's primary group. This is the group that will be assigned group ownership of the user's files by default.

# Selecting a Good Password

When you create an account, you typically should create a password for it. Sometimes, the user can select the password when the account is created. Other times, you'll need to select a password that the user will use initially. In such cases, instruct the user to change the password as soon as possible. In either case, it's important to educate users about selecting a good password. Poor common passwords include those based on the following:

Be sure to follow the advice in this section, especially for the root password!

- The names of family members
- Favorite books, movies, television shows, or the characters in any of them
- Telephone numbers, street addresses, or Social Security numbers
- Any other meaningful personal information

# Creating New Accounts

- Any single word that's found in a dictionary (in any language)
- Any simple keyboard or alphanumeric combination, such as qwerty or 123456

The best possible passwords are random collections of letters, digits, and punctuation. Unfortunately, such passwords are difficult to remember. A reasonable compromise is to build a password in two steps:

1. Choose a base that's easy to remember but difficult to guess.
2. Modify that base in ways that increase the difficulty of guessing the password.

One approach to building a base is to use two or more unrelated words, such as bun and pen. You can merge these two words (bunpen). Another approach, and one's arguably better than the first, is to use the first letters of a phrase that is meaningful to the user. For instance, the first letters of "yesterday" I went to the "dentist" are yytd. In both cases, the base should not be a word in any language. As a general rule, the longer the password, the better.

With the base in hand, it's time to modify it to create a password. The user should apply at a couple of possible modifications:

**Adding Numbers or Punctuation** One important change is to insert random numbers or punctuation in the base. This step might yield, for instance, bu3pn7 or yytd. As a general rule, add at least two symbols or numbers.

**Mixing Case** Linux uses case-sensitive passwords, so jumbling the case of letters can improve security. Applying this rule makes Bu3nPE?n and y+19wttD, for instance.

**Reversing Order** A change that's very weak by itself but can add security when used in conjunction with the others is to reverse order of some or all letters. You might apply this to just one of a two-word base. This could yield Bu3nn?EP and Dtt99I+, for instance.

**Growing the Haystack** An intruder's trick of discovering a password has been linked to finding a needle in a haystack. One way to make this task harder is to increase the size of the haystack. In password terms, this means making a password larger. You can do this by using larger words or phrases, course, but this can make a password harder to remember and type. Even a size that simply repeats a single character can be helpful. You thus might turn the passwords into Bu3nn?EP11111iiii or DttIIIIIIIIW91+.

![](img/77662199428609b7662c8dc9c0e45c10_268_0.png)

# Chapter 13 • Creating Users and Groups

Your best tool for getting users to pick good passwords is to educate them.
Here are some insights to share with users:

- Passwords can be guessed by malicious individuals who know them or even who target them and look up personal information on social media, web-based telephone directories, business profiles, and so on.
- Although Linux salts and hashes its internally, programs that feed entire dictionaries through Linux's salting/hashing algorithms for comparison to a Linux system's passwords. If a match is found, the password has been found.
- User accounts might be used as a first step towards compromising the entire computer or as a launching point for attacks on other computers.
- Users should never reveal their passwords to others, even people claiming to be system administrators. This is a common scam, because real system administrators don't need users' passwords.
- The same password should not be used on multiple systems, because doing so quickly turns a compromised account on one computer into a compromised account on all of them.
- Writing passwords down or emailing them are both risky practices. Writing a password on a sticky note stuck to the computer's monitor is particularly foolish.

Telling your users these things will help them understand the reasons for your concern, and it's likely to help motivate at least some of them to pick good passwords.

# DON'T USE THESE PASSWORDS!

If you do a search on common passwords or a similar phrase, you'll quickly discover websites that provide surveys showing the most typical and easily guessed passwords that security researchers have uncovered. Details vary from one to another, but typically common passwords include the following:

- 123456
- password
- 12345678

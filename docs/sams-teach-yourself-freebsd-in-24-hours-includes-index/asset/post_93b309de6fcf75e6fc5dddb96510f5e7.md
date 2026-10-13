
![](img/ba0161b65b37e94cffc801ecbacaba5e_104_0.png)

> Never create a user account with a UID of 0. The UID 0 is reserved for the root user, which means that any user account you create with UID 0 will have root privileges on the system!

```
Login group fbar [fbar]:
```

This will be the user's primary group. Until you know more about groups, it is best to leave this as the default. By default, FreeBSD gives each user his own group. If you want to give users access to other groups, you can make them members of secondary groups. You will learn more about that later in this hour in the section on groups.

```
Login group is 'fbar'. Invite fbar into other groups: guest no [no]:
```

I suggest that you leave this question alone for now and just accept the default. It is very easy to add the user to other groups later on.

```
Use password based authentication (y/n) [y]: y
Use an empty password (y/n) [n]: n
```

Select y to the first question and n to the second question: Otherwise, you will end up creating an account that can be logged in to without a password. This is almost never a good idea. An example of where you might want something like this is with a guest account that has restricted privileges, can only run a single program, and so on.

```
Enter password []:
Enter password again []:
```

There was a time when passwords were restricted to a maximum of eight characters. However, this limit no longer applies these days.

The importance of creating strong passwords cannot be overemphasized. The security of a system is only as strong as its weakest link, and weak passwords are often the weakest link. All too often, users will choose passwords such as the name of their child, pet, city of birth, and things that other people know or can easily find out about them. It's also fairly common for people to write down their password on a Post-It note and then stick it under their desk, keyboard, or even worse, directly on the side of the monitor. It is important that you discourage this kind of behavior because bottoms of desks and keyboards are the first place someone who wants to steal a password will look. Here is a list of guidelines for creating secure passwords:

- Passwords should be at least eight characters long.
- Use a mixture of upper- and lowercase letters, numbers, and at least one special character in passwords. This will help foil programs that try random words to crack a password through brute force methods.
- Don’t use words that are in the dictionary because there are programs that will try random words to attempt to find a valid password.
- Don’t use information that other people know or can easily find out about you.
- Use something that will be easy for you to remember, but difficult for others to guess. Things that are hard for you remember encourage the bad practice of writing the password down and storing it somewhere. Some ways of doing this include combining parts of two or more words that mean something to you but won’t mean anything to anyone else and will not make sense when combined. Another possibility is substituting the character next to or above the real character in the word. In this case, you will end up with a password that is total nonsense but will still be easy to remember as long as you remember the substitution key you used.
- Make sure your users understand that no one from your company will ever call or email them and ask them for their password. Users receiving calls and email from people claiming to be from IT and asking the user for his password is a very common method of cracking systems. Many users will actually give the caller or sender the password.

After you have entered and verified the password, select y to answer the question about enabling the password at account creation. You will then be given a list of details about the account and asked if you are sure that they are all correct. Assuming that they are, select y. Next, you will be asked if you want to send the new user an email message. As mentioned before, the default message that will be sent is /etc/adduser/message. You can use this message to give the new user information about who to contact for help, system use policies, and so on.

After you have finished answering the questions about sending the message, the account will be created and you will be asked if you want to create another account. Simply answer yes or no, and you are done.

## Removing a User Account

If you need to remove a user account from the system, use the rmuser command. An example is shown here:

```
rmuser fbar
Matching password entry:
fbar:DKN1lrd/diQRj:1002:1002::0:0:Foo Bar:/home/fbar::/usr/local/bin/ksh

Is this the entry you wish to remove? Y
Remove user’s home directory (/home/fbar)? Y
```

```
Updating password file, updating databases, done.
Updating group file: (removing group fbar : - personal group is empty) done.
Removing user's home directory (/home/fbar): done.
Removing files belonging to fbar from /tmp: done.
Removing files belonging to fbar from /var/tmp: done.
Removing files belonging to fbar from /var/tmp/vi.recover: done.
```

Most of this is fairly self-explanatory. The question about whether you want to remove the user's home directory deserves some further discussion, though. Why might you want to keep a user's home directory around? The main reason would be if someone left the company, but they had files in their directory relating to duties that a new employee was going to take on. In this case, you would want to preserve the old user's home directory while deleting his account. You could then change the ownership of the files to the new employee who will take on the duties.

## Groups and Their Purpose

To provide more flexibility, FreeBSD also supports groups. Groups allow multiple users to have access to a file or directory while denying people who are not members of the group access to the file or directory. Here is an example of when this might be useful.

Suppose that you have a sales and a marketing department. The marketing department is working on some new flyers and other marketing materials. Five people are on the marketing team who all need to be able to read and write to the files. You also have a sales department with five people in it. The sales department should be able to read the new marketing flyers. However, they should not be able to make any changes to them. Furthermore, you have some experimental marketing ideas that your five marketing people are collaborating on for an experimental new marketing strategy. This needs to be strictly kept under wraps, and you don't want the sales people to have access to it yet. Also, suppose that the sales people has access to a file that contains customers' phone numbers. We don't want the marketing people to have access to this: Only the sales people should be able to access it.

The first thing we will want to do is create two groups. We can call one sales and the other market. Then we will add each of our users to the appropriate group.

## Creating Groups

To create a new group, simply add an entry to the /etc/group file that contains the name of the group, a GID number, and a list of users who belong to the group. Here are two sample entries for the new groups we want to create:

```
sales:*:1005:john, joe, frank, dave, susan
market:*:1006:lynn,peter,dave,sara,alice
```

As with user ID numbers, group ID numbers for normal groups should be higher than 1,000. It is also important to make sure that there are no duplicate group ID numbers. Each field is separated by a colon. The first field contains the name of the group. The second field contains an asterisk, which is a place holder that primarily exists for historical reasons. The third field contains the group ID number, or GID, and the final field contains a list of all usernames who are members of that group. Notice that the user dave is a member of both groups. This is perfectly acceptable. In this example, suppose that Dave is the exception to the rule. He is a sales person who, for whatever reason, needs full access to the material reserved for marketing people.

After you have created the groups, you need to set the appropriate directory and file permissions and make sure that they are owned by the appropriate people.

![](img/ba0161b65b37e94cffc801ecbacaba5e_107_0.png)

> For the curious, the asterisk placeholder mentioned previously exists from a time when users could not be members of more than one group at any given time, so they had to change their group membership anytime they wanted to access a different group. This field used to hold the password for changing into the new group.

## Changing the Group Ownership

The command to change the group owner of a file or directory is chgrp. For example, to change the customer-data file to be owned by the sales group, you would use the following command:

```
chgrp sales customer-data
```

The command always takes the name of the group that the file or directory should be changed to, followed by the name of the file or directory that you want to change.

![](img/ba0161b65b37e94cffc801ecbacaba5e_107_1.png)

> Only the owner of a file or the root user can change the group that the file belongs to. And the owner can only change the group to a group that he is a member of. Of course, the root user can change the group membership of a file to any group, regardless of whether root is the owner of the file or is a member of the group that the file is being changed to.

Repeat the previous command for each file or directory that you want to change the group ownership of. Also, repeat the same procedure for the market group.

![](img/ba0161b65b37e94cffc801ecbacaba5e_107_2.png)

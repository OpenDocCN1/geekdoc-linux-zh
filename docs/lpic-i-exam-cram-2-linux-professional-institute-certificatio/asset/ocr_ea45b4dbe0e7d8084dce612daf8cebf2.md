2 bits to be on, or rw (read and write). If you see a file that is set to 666, that equates to all three trios having the same permissions—read and write.

> Watch for questions that try to trick you with a user who's both the user owner and a member of the group owner, but the correct permissions for executing or changing the file aren't in a single trio. You can't mix the trios, even if your profile encompasses several of the trios.

For example, say a user named fred is the user owner of the file object /home/fred/22AcaciaAvenue.mp3 and is also a member of the group owner of that object. The file's listing has the following permissions set:

```
-rw-r-xr-x 2 fred users 0 Jan 26 13:08 22AcaciaAvenue.mp3
```

fred's permissions might seem to span the various trios, but because fred is the user owner, he matched the first trio and stopped there.

# Manipulating Permissions

chmod is the command to use when modifying or altering an object's permission trio bits. Only the root and object owners can alter permissions.

The two modes of manipulating the permissions for an object are numeric and symbolic. Both modes have their place, and if there were only one mode, someone would have to invent the other, just for variety.

# Numeric Mode

Numeric permissions are the most often used, and they appear on the exam with greater frequency than the symbolic style. As a rule, I recommend using the numeric mode to set or force permissions on an object. For example, if you are told that the current permissions for an object are 644 and you are asked to ensure that all users have read and write access to that object, you can assume that the numeric style is correct, as shown here:

```
chmod 666 file
```

The chmod command works great on groups of files, too:

```
chmod 644 /home/lukec/*.txt
```

It even works on directories and their contents. For example, say the user bertrandr has a home directory he inherited from someone else and a few files are not set properly to be readable only by him. He asks you to set all the files in his home directory to 640 for security's sake and to give him read/write access to them. You might use the command:

```
chmod -R 640 /home/bertrandr/*
```
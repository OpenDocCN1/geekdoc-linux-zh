
# The Linux Cookbook: Tips and Techniques for Everyday Use:

Brackets also have special meaning when used in conjunction with other characters, as described by the following table.

# CHARACTER DESCRIPTION

–
A hyphen as part of a bracketed list denotes a range of characters to match—so `[a-m]` matches any of the lowercase letters from `a` through `m`. To match a literal hyphen character, use it as the first or last character in the list. For example, `a[-b]c` matches the files `a-c` and `abc`.

!
Put an exclamation point at the beginning of a bracketed list to match all characters except those listed. For example, `a[!b]c` matches all files that begin with an `a` character, end with a `c` character, and have any one character, except a `b` character, in between; it matches `aac`, `a-c`, `adc`, and so on.

You can combine these special expansion characters in any combination, and you can specify more than one pattern as multiple arguments. The following examples show file expansion in action using commands described in this chapter.

- To list all files in the `/usr/bin` directory that have the text `tex` anywhere in their name, type:
  
  `$ ls /usr/bin/*tex* RET`

- To copy all files whose names end with `.txt` to the `doc` subdirectory, type:
  
  `$ cp *.txt doc RET`

- To output a verbose listing of all files whose names end with either a `.txt` or `.text` extension, sorting the list so that newer files are listed first, type:
  
  `$ ls -lt *.txt *.text RET`

- To move all files in the `/usr/tmp` directory whose names consist of the text `song` followed by an integer from 0 to 9 and a `.cdda` extension, placing them in a directory `music` in your home directory, type:
  
  `$ mv /usr/tmp/song[0-9].cdda ~/music RET`

- To remove all files in the current working directory that begin with a hyphen and have the text `out` somewhere else in their file name, type:
  
  `$ rm -- -*out* RET`

- To concatenate all files whose names consist of an `a` character followed by two or more characters, type:

## 7. Sharing Files

Groups, file ownership, and access permissions are Linux features that enable users to share files with one another. But even if you don't plan on sharing files with other users on your system, familiarity with these concepts will help you understand how file access and security work in Linux.

- 7.1 Groups and How to Work in Them
  How users can work together in groups.
- 7.2 File Ownership
  Who owns a file?
- 7.3 Controlling Access to Files
  Who has permission to access a file?

## 7.1 Groups and How to Work in Them

A group is a set of users, created to share files and to facilitate collaboration. Each member of a group can work with the group's files and make new files that belong to the group. The system administrator can add new groups and give users membership to the different groups, according to the users' organizational needs. For example, a system used by the crew of a ship might have groups such as galley, deck, bridge, and crew; the user captain might be a member of all the groups, but user steward might be a member of only the galley and crew groups.

On a Linux system, you're always a member of at least one group: your login group. You are the only member of this group, and its group name is the same as your username.

Let's look at how to manage your group memberships.

- 7.1.1 Listing the Groups a User Belongs To
  Listing the groups a user is a member of.
- 7.1.2 Listing the Members of a Group
  Listing the members of a group.

## 7.1.1 Listing the Groups a User Belongs To

To list a user's group memberships, use the groups tool. Give a username as an argument, and groups outputs a line containing that username followed by all of the groups the user is a member of. With no arguments, groups lists your own username and group memberships.

- To list your group memberships, type:

```
$ groups RET
steward galley crew
$
```

In this example, three groups are output: `steward` (the user's login group), `galley`, and `crew`.

- To list the group memberships of user `blackbeard`, type:

```
$ groups blackbeard RET
blackbeard : blackbeard
$
```

In this example, the command outputs the given username, `blackbeard`, followed by the name of one group, `blackbeard`, indicating that user `blackbeard` belongs to only one group: his login group.

---

[<] [>] [<<] [Up] [>>] [Top] [Contents] [Index] [?]

## 7.1.2 Listing the Members of a Group

@sf(Debian): `members`

To list the members of a particular group, use the members tool, giving the name of the particular group as an argument.

- To output a list of the members of the `galley` group, type:

```
$ members galley RET
captain steward pete
$
```

In this example, three usernames are output, indicating that these three users are the members of the `galley` group.

---

[<] [>] [<<] [Up] [>>] [Top] [Contents] [Index] [?]

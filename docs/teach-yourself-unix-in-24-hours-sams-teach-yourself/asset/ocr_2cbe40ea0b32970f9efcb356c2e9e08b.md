# Hour 10

Here I'm using awk to extract just the seventh field of the password file, the home directory, handing them all to the sort program. I then let uniq figure out which ones occur how often and, with -c, report the count of occurrences to me. This is true on your system, too.

+   4. Sticking with the password file, notice that the names are all in first-name-then-last name format. That is, my account is Dave Taylor,.... A common requirement that you might have to generate a report of system users. You'd like to sort them by name, but by last name. You do it with awk, of course:

```
% grep taylor /etc/passwd | awk -F: '{print $5}'
James Taylor,....
Mary Taylor,....
Dave Taylor,....
James Taylor,....
Robert Taylor,....
Melanie Taylor,....
Dave Taylor,....
```

That generates the list of users. Now I'll use sed to remove those annoying commas and awk to reverse the order of names:

```
% grep taylor /etc/passwd | awk -F: '{print $5}' | sed 's/,///g'
| awk '{print $2"," $1"}'
Taylor, James
Taylor, Mary
Taylor, Dave
Taylor, James
Taylor, Robert
Taylor, Melanie
Taylor, Dave
```

If I could feed the output of this command to sort, the names will finally be listed in the order desired:

```
% grep taylor /etc/passwd | awk -F: '{print $5}' | sed 's/,///g'
| awk '{print $2"," $1"}' | sort
Taylor, Dave
Taylor, Dave
Taylor, James
Taylor, James
Taylor, Mary
Taylor, Melanie
Taylor, Robert
```

This is slick. It also illustrates how you can use various UNIX commands increasingly to build up your desired result.
5. The script earlier that looked for the login shell isn't quite correct. It turns out that if the user wants to have /bin/sh—the Bourne shell—as his or her default shell, the final field can be left blank:

```
joe:?:45:555:Joe-Bob Billiard,....:/home/joe:/bin/sh:/bin/sh
```

![](bbox=[0.06, 0.883, 0.143, 0.963])
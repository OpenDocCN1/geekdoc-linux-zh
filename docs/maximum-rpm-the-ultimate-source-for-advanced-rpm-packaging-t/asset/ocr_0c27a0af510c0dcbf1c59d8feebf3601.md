Let’s put together a format string that will display the package name, followed by the name of every file that package contains. We’ll try it on the adduser package first since it contains only one file:

```
# rpm -q --queryformat '%{NAME}: %{FILENAMES}\n' adduser adduser: /usr/sbin/adduser #
```

Hey, not bad: Got it on the first try. Now let’s try it on a package with more than one file:

```
# rpm -q --queryformat '%{NAME}: %{FILENAMES}\n' etcskel etcskel: (array) #
```

Hmmmm. What went wrong? It worked before. Well, it worked before because the adduser package contained only one file. The FILENAMES tag points to an array of names, so when there is more than one file in a package, there’s a problem.

But there is a solution. It’s called an iterator. An iterator can step through each entry in an array, producing output as it goes. Iterators are created when square braces enclose one or more tags and literal text. Since we want to iterate through the FILENAMES array, let’s enclose that tag in the iterator:

```
# rpm -q --queryformat '%{NAME}: [%{FILENAMES}]\n' etcskel etcskel: /etc/skel /etc/skel/.Xclients /etc/skel/.Xdefaults /etc/skel/.ba #
```

There was more output: It went right off the screen in one long line. The problem? We didn’t include a newline escape sequence inside the iterator. Let’s try it again:

```
# rpm -q --queryformat '%{NAME}: [%{FILENAMES}\n]' etcskel etcskel: /etc/skel /etc/skel/.Xclients /etc/skel/.Xdefaults /etc/skel/.bash logout /etc/skel/.bash profile /etc/skel/.bashrc /etc/skel/.xsession #
```

That’s more like it. If we wanted, we could put another file-related tag inside the iterator. If we included the FILESIZES tag, we’d be able to see the name of each file, as well as how big it was:

```
# rpm -q --queryformat '%{NAME}: [%{FILENAMES} (%{FILESIZES} bytes) \n]\' > etcskel etcskel: /etc/skel (1024 bytes) /etc/skel/.Xclients (551 bytes) /etc/skel/.Xdefaults (3785 bytes) /etc/skel/.bash logout (24 bytes) /etc/skel/.bash profile (220 bytes) /etc/skel/.bashrc (124 bytes) /etc/skel/.xsession (9 bytes) #
```

That’s pretty nice. But it would be even nicer if the package name appeared on each line, along with the filename and size. Maybe if we put the NAME tag inside the iterator:
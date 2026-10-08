
Licensing restrictions and intellectual property laws occasionally have stymied the growth of UNIX. Although UNIX is unquestionably popular with programmers, these same programmers have a burning desire to see what's inside, to learn about how UNIX works by examining UNIX itself. UNIX is owned by AT&T. Few people are able to view the source legally. Those who look into UNIX are "tainted": Anything they write in the future may be inspired by proprietary code of AT&T. The situation is fuzzy in many ways, and that's where the Free Software comes in. The brainchild of Richard Stallman, the FSF is slowly rewriting all the major utilities and then distributing them with the source, as part of the ambitious GNU project. GNU emacs is one example, and the Bourne shell is another.

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_317_0.png)

## JUST A MINUTE

- In Hour 9 you learned how to use awk to extract the default login of each user on your system and then use sort and uniq to collate the data and present an attractive output, respectively. Armed with the description of all the different shells, you can now take another:

```
awk -F: '{print $7}' /etc/passwd | sort | uniq -c
2
3361 /bin/csh
1 /bin/false
85 /bin/ksh
21 /bin/bash
11 /usr/local/bin/ksh
361 /usr/local/bin/tcsh
7 /usr/local/bin/nsh
```

- You can see that the vast majority of the people on this system uses the C shell. To look at it a different way, compute the number of entries in the password file:

Now, what percentage of users have chosen each of these shells? This is a job for bc:

```
% bc
x=3849
scale=4
3361/x*100
87.3200
85/x*100
2.2000
361/x*100
9.3700
^c
```

It's a tad difficult to interpret, but this output says that 87.3 percent of the users have csh as their login shell, another 9.4 percent used the modified tcsh, and only 2.2 percent use ksh. The remaining 1.1 percent use either the Bourne shell or the MH shell, or they default to the Bourne shell (the two accounts in the preceding output, without any shell indicated).

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_317_1.png)

## Hour 14

# Introduction to Command Shells

> The scale=4 command tells bc how many digits to display after the decimal point in numbers. By default, unfortunately, bc displays no digits after the decimal point.

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_318_0.png)

Quite a variety of shells is available, the most common one on sites I familiar with is the C shell. Clearly, the system that I used for this particular set of examples has an overwhelming majority of C shell users: A combined of 97 percent of the users are working within the C shell or descent tsh.

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_318_1.png)

# Task 14.2: Identifying Your Shell

There are many different approaches to identifying shell you're using. The easiest, however, is just to swoop into the /etc/passwd file to see what your account lists. It's helpful to know some alternatives because the /etc/passwd isn't always available (some systems don't have an /etc/passwd file in the interest of security).

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_318_2.png)

- 1. One simple technique to identify your shell is to check your prompt. If your prompt contains a $, you probably are using the C shell or modified C shell (tsh). If your prompt contains #$, you could be using the Bourne shell, the Korn shell, or a variant thereof.
- 2. A more reliable way to ascertain which shell you're using is to ask the operating system what you're currently running. The shell identifies the ID of the shell. You can use $$ as a search pattern for grep on the output of ps to see what shell you are using. Here's what happens when I try:

```
$ ps -ef | grep $$
taylor 26905 0.0 0.2 256 144 Ai S 0:03 -csh (csh)
taylor 29751 0.0 0.1 52 28 Ai S 0:00 grep 26905
```

You can see that I'm running the C shell. Using $$ in this fashion also matches the grep process (notice that the $$ have expanded to the current shell process identification, 26905). There is a leading dash on the indication of whether is my login shell or just a shell that I'm running.

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_318_3.png)

- 3. Another way to find out what shell I'm running is to peek into the /etc/passwd file, which you can do with some sophistication that awk is no longer a mystery.

```
% awk -F: ' if ($1 == "taylor") print "your shell is: \$7" ' < /etc/passwd
nyour shell is: /bin/csh
```

- 4. The best way to figure out what shell you're running, however, is to use csh. Learn how to use csh in the following task.

Once you've identified your shell, you can contemplate choosing a different one.

# Task 14.3: How To Choose a New Shell

In the past, the only way to switch login shells on many systems was to ask the system administrator to edit the /etc/passwd file directly. This usually meant waiting until the administrator had time. The good news is that there's a simple program (almost all UNIX systems) to change login shells—it's csh, or change csh. It has no starting flags or options.

- 1. The first step is to identify what shells are available. By convention, shells are located in /bin or /usr/bin. You can use the ls command to see what's there:

```
$ ls /bin
bash
csh
dash
ksh
sh
```

- 2. If you have csh on your system, you might be interested in experimenting with this different shell. To change my login shell to any of these shells, or even just to verify I'm running, I can use the change shell command:

```
% chsh
```
```

- 3. Unfortunately, it requires you to specify one. I'll try to confuse you by requesting emacs become my login shell:

```
% chsh
Changing shell for taylor.
Old shell: /bin/csh
New shell: /usr/local/bin/gnuacs
/usr/local/gnuacs is unacceptable as a new shell.
```

- 4. The program has some knowledge of valid shell names. You can peek into the file that etsh uses to confirm which programs are valid shells. I'll check /etc/shells and looks like this:

```
% cat /etc/shells
/bin/ksh
/bin/sh
/bin/csh
/usr/local/bin/csh
/usr/local/bin/tcsh
```

- 5. If you have csh on your system, you might be interested in experimenting with this/bin/tcsh. I'll change my login shell from /bin/csh to /usr/local/bin/tcsh:

```
% chsh
Changing login shell for taylor
Old shell: /bin/csh
New shell: /usr/local/bin/tcsh
```

Notice that, in UNIX style, there is no actual confirmation that anything was done. Fortunately, I can easily check by using etsh again or redoing the awk program with a C shell history command:

```
% ialah -F: '{if ($1 == "taylor") print "your shell is: " $7}' < /etc/passwd
your shell is: /usr/local/bin/tcsh
```

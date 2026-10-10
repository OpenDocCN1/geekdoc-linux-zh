Does it work? Let’s invoke it:

```
$ private_buc<Enter>
$ ls -l /nightly<Enter>
total 12
-rw-rw-r-- 1 freston knights4 8299 Jul 14 16:44 freston-backup-20010714.tgz
```

Well, we can tell you that it worked. Try it.

# ## Conditionals

We mentioned earlier that sometimes you need to test for a condition—that is, to see whether it something true or not—before proceeding with a script. The use of conditionals like this is quite simple and the conditionals generally use combinations or variations of “if,” “then,” and “else” expressions. These conditionals can use many forms but at the same time must abide by some simple rules.

# ### If, Then, Else

The simplest form of a conditional is just if and then, as follows: “If this happens, then do that.” The if part has to be true, though. Otherwise, it is ignored. Sometimes this simple “if . . . then” is all you need.

When this statement is not enough, you can add else: “If this happens to be true, then do the following. For all those that are false, then do else.” Think of each of these elements as being people. Mr. If decides whether it is true or false. If it is true, Mr. If will give the work to Mr. Then. If it is false, then Mr. If will give the work to Ms. Else. The beauty of Mr. If’s job is that everything is either true or false. No matter what the response is, he gets to hand the rest of the job off to somebody else.

The only other thing that we will mention before showing some examples is that there are many forms of the use of if, then, and else in other programming environments. Unless you want to make a career out of memorizing when a finish is required and when it is not required, just use it. At the end of every if, then, and else should be an fi.

#### Example 13.12 The Modified Simple Backup Script
Freston modified the script from the previous example to check for “disk full” before backing up files in the home directory. Look for the “if . . . then . . . else” sequence:
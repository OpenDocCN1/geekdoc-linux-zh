alias command.\" Then, he offers to show Sancho how to create an alias called “linkcheck,” which is similar to the one he (Freston) uses to check for file links:

```
$ alias linkcheck='find . -type f -links 2 | xargs ls -1i'<Enter>
```

After that, all Sancho would have to do is cd to his own home directory and then enter

```
$ linkcheck<Enter>
13444 -rw-r-r--- 2 panzasan knightal 144 Jul 11 11:42 ./knightdata
16698-rw-r---2 quixoted knightal 605 Jul 21 15:35 ./dapple_poem
18138-rw-r---2 quixoted knightal 392 Jul 17 14:37 ./roz_song
```

# Example 9.10 Removing Old Files with an alias Command

In Example 9.3, we saw how Freston combined find, xargs, and rm to search for files with modification dates older than 30 days so that he can remove them from the system.

He has created an alias command called oldrm to achieve the same objectives and to save time. Here is how he created that alias command:

```
$ alias oldrm='find . -type f -mtime +30 | xargs rm'<Enter>
```

Notice that he has left off the -t (verbose) option. Freston, a long-time Linux/UNIX user, does not really need to minutely monitor the rm process.

So now, Freston enters the following code to find and remove old files:

```
$ oldrm<Enter>
rm ./oldfileX ./oldfileY ./oldfiles ./oldfilesa etc....
```

# Determining File Types: The file Command

The file command is used to classify a file according to its content. This command uses up to three tests:
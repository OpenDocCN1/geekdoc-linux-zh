Unfortunately I have unintentionally overwritten what was already contained in echo-out.txt. There's no undo button in Unix so I'll have to live with this mistake. This is the first of several lessons demonstrating the damage that you should try to avoid inflicting with Unix. Make sure to take extra care when executing commands that can modify or delete a file, a typo in the command can be potentially devastating. Thankfully there are a few strategies for protecting yourself from mistakes, including managing permissions for files, and tracking versions of your files with Git, which we will discuss thoroughly in a later chapter.

Finally we should discuss how to edit text files. There are several file editors that are available for your terminal including vim⁴ and emacs⁵. Entire books have been written about how to use both of these text editors, and if you're interested in one of them you should look for resources online about how to use them. The one text editor we will discuss using is called nano. Just like less, nano uses your entire terminal window. Let's edit todo.txt using nano:

```
nano todo.txt
```
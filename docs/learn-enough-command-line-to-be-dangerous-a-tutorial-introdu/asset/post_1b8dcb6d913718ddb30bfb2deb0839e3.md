
| Command | Description | Example |
|---|---|---|
| mkdir <name> | Make directory with name | `$ mkdir foo` |
| pwd | Print working directory | `$ pwd` |
| cd <dir> | Change to <dir> | `$ cd foo/` |
| cd ~/ <dir> | cd relative to home | `$ cd ~/foo/` |
| cd | Change to home directory | `$ cd` |
| cd - | Change to previous directory | `$ cd && pwd && cd -` |
| . | The current directory | `$ cp ~/foo.txt .` |
| .. | One directory up | `$ cd ..` |
| find | Find files & directories | `$ find . -name foo*.*` |
| cp -r <old> <new> | Copy recursively | `$ cp -r ~/foo .` |
| rmdir <dir> | Remove (empty) dir | `$ rmdir foo/` |
| rm -rf <dir> | Remove dir & contents | `$ rm -rf foo/` |
| grep -ri <string> <dir> | Grep recursively (case-insensitive) | `$ grep -ri foo bar/` |

Table 5: Important commands from Section 4.

## Exercises

- 1. Using a single command-line command, make a directory **foo**, change into it, create a file **bar** with content "baz", print out **bar**'s contents, and then `cd` back to your home directory. *Hint: Combine the commands as described in Box 12.*
- 2. What happens when you run the previous command again? How many of the commands executed? Why?
- 3. Explain why the command `rm -rf /` is unbelievably dangerous, and why you should never type it into a terminal window, not even as a joke.
- 4. How can the previous command be made even more dangerous? *Hint: Refer to Box 11. (This command is so dangerous you shouldn't even think it, much less type it.)*

## 5 Conclusion

Congratulations! You’ve officially learned enough command line to be *dangerous*. Of course, this is only one step on a longer journey, both toward command-line excellence (Box 13) and software development wizardry. As you proceed on this journey, you will probably discover that learning computer magic can be exciting and empowering, but it can also be *hard*. Indeed, you may already have discovered this fact, either on your own or while doing this tutorial. To those brave magicians-in-training who wish to proceed, I offer the following sequence, which is currently in preparation:

- 1. **Software development foundations**
  - (a) *Learn Enough™ Command Line to Be Dangerous* (you are here)
  - (b) *Learn Enough™ Text Editor to Be Dangerous*
  - (c) *Learn Enough™ Git to Be Dangerous*
- 2. **Web technology basics**
  - (a) *Learn Enough™ HTML to Be Dangerous*
  - (b) *Learn Enough™ CSS to Be Dangerous*
- 3. **Ruby web development track**
  - (a) *Learn Enough™ Ruby to Be Dangerous*
  - (b) *Learn Enough™ Ruby Web Development to Be Dangerous*
  - (c) *Learn Enough™ Ruby on Rails to Be Dangerous*
- 4. **Professional-grade Ruby web development**
  - *The Ruby on Rails Tutorial*

Only the first and last titles in the above list are complete, but all the other links go to landing pages where you can sign up to be notified when the next tutorial in the sequence is ready. See you there!

## Box 13. Additional resources

I recommend following the Learn Enough™ sequence, as it represents the shortest path to technical proficiency and software development skills, but at some point you’ll probably want to expand your command-line skills as well. When that time comes, I recommend consulting this list, which consists mainly of resources recommended by readers of the present tutorial:

- * Conquering the Command Line book and screencasts by Mark Bates (which like the present tutorial is available for free online)
- * edX course on Linux
- * Codecademy course on the command line
- * The similarly named The Command Line Crash Course and A Command Line Crash Course
- * Learning the Shell

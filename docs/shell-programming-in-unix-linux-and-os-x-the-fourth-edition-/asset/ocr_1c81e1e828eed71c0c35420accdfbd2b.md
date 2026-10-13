exception of some Bash examples in Chapter 14, were run using the Korn shell, although all of them also work fine with Bash.

Because the shell offers an interpreted programming language, programs can be written, modified, and debugged quickly and easily. We turn to the shell as our first choice of programming language and after you become adept at shell programming, you will too.

# How This Book Is Organized

This book assumes that you are familiar with the fundamentals of the system and command line; that is, that you know how to log in; how to create files, edit them, and remove them; and how to work with directories. In case you haven’t used the Linux or Unix system for a while, we’ll examine the basics in Chapter 1, “A Quick Review of the Basics.” In addition, filename substitution, I/O redirection, and pipes are also reviewed in the first chapter.

Chapter 2, “What Is the Shell?,” reveals what the shell really is, how it works, and how it ends up being your primary method of interacting with the operating system itself. You’ll learn about what happens every time you log in to the system, how the shell program gets started, how it parses the command line, and how it executes other programs for you. A key point made in Chapter 2 is that the shell is just another program; nothing more, nothing less.

Chapter 3, “Tools of the Trade,” provides tutorials on tools useful in writing shell programs. Covered in this chapter are cut, paste, sed, grep, sort, tr, and uniq. Admittedly, the selection is subjective, but it does set the stage for programs that we’ll develop throughout the remainder of the book. Also in Chapter 3 is a detailed discussion of regular expressions, which are used by many Unix commands, such as sed, grep, and ed.

Chapters 4 through 9 teach you how to put the shell to work for writing programs. You’ll learn how to write your own commands; use variables; write programs that accept arguments; make decisions; use the shell’s for, while, and until looping commands; and use the read command to read data from the terminal or from a file. Chapter 5, “Can I Quote you on That?”, is devoted entirely to a discussion of one of the most intriguing (and often confusing) aspects of the shell: the way it interprets quotes.

By that point in the book, all the basic programming constructs in the shell will have been covered, and you will be able to write shell programs to solve your particular problems.

Chapter 10, “Your Environment,” covers a topic of great importance for a real understanding of the way the shell operates: the environment. You’ll learn about local and exported variables; subshells; special shell variables, such as HOME, PATH, and CDPATH; and how to set up your .profile file.

Chapter 11, “More on Parameters,” and Chapter 12, “Loose Ends,” tie up some loose ends, and Chapter 13, “Rolo Revisited,” presents a final version of a phone directory program called rolo that is developed throughout the book.
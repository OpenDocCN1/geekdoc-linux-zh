situations where different utilities give opposite meanings to different commands, e.g., vi interpets "quit" to mean finish without updating the file and "exit" to mean finish after updating the file, while mail in-terpets "quit" to mean finish after updating the mail queue and "exit" to mean finish without updating the mail queue.

Linux, Unix, and other Unix-like systems have been properly criti-cized for this confusion, but the best we can hope for is a gradual con-vergence towards consistent interpretations. We must remember that the command language at any moment is a function of which program is in control of the terminal.

# ### 3.1.1 Shells

A shell is almost always the primary interface between Linux and the user.

There are over a dozen different shells, each having a language which differs from the others in a number of subtle ways. These language differences (or improvements as claimed by some) are called *syntactic sugar* by many, suggesting the differences have little substance, but they make the use a lot “sweeter”. Although the differences don’t signific-antly extend the ultimate ability of the languages, there are strong ad-herents for different languages. This is because some more conveniently express what the programmer intends and others provide a comfortable, stable work place.

I’ll try to stay out of this religious battleground and instead try to focus on the major elements common to most of the languages. There are two major shell families, named after the first of their lines—the Bourne shell and the C shell. When appropriate, examples for each will be given.

The novice user sees the language in terms of single line commands. At this most basic level, the shell serves to let the user invoke the ex-ecution of application programs, one at a time. Some of these programs can be rather extensive, e.g., a database client or server, a text editor or formatting utility, compilers and linkers, or terminal emulators. Other commands are more mundane, e.g., display the date, list the directory contents, move or copy a file, or assign a value to a variable.
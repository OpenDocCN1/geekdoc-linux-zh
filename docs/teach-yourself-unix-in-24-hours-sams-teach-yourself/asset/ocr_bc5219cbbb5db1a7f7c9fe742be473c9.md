# Wildcards and Regular Expressions

letteracy
letterate
Papert
pre
rithmetic
Rs

You have now met the entire family of grep commands. For the majority of searches for information, you can use the grep command itself. Sometimes, though, it's nice to have options, particularly if you decide to customize some of your commands as shown in the scripts and aliases explained in this hour.

# Task 9.7: Changing Things En Route with sed

I'm willing to bet that when you read about learning some UNIX programming tools in this, you anxious, your palms started to get sweaty, maybe your fingers shook, and the little voice in your head started to, “It's too late! We can use a pipe and paper! We don't need computers at all!

Don't panic.

If you think about it, you've programming all in UNIX. When you enter a command to the shell, you're programming the shell to perform immediately the task specified. When you specify file redirection or build a pipe, you're really writing a small UNIX program that the shell interprets and acts upon. Frankly, when you consider how many commands you know now and how many flags there are for each of the commands, you've quite a set of programming tools under your belt already, so onward!

With the | symbol called a pipe, and commands tied called pipelines, is it no wonder that the information flowing down a pipeline is a stream? For example, the command `cat test | wc` means that the cat command opens the file test and streams it to the wc, which counts the number of lines, words, and characters.

To edit, modify the information in a pipeline, then it seems reasonable to use a stream editor, and exactly what the sed command is! In fact, its name comes from its function: s for stream, and ed for editor.

Here's how the sed command is built on an old editor ed, the same editor that's responsible for the grep command Remember? The `global/regular expression/` prints exactly grep. A microcosm of unix itself, commands sed to separated by a semicolon.

There are many different sed commands, but keeping with my promise not to overwhelm you with options and variations that aren't going to be helpful, I'll focus on using sed to substitute one pattern for another and for extracting ranges of lines from a file. The general format of the substitution command is: `s/old/new/flags`, where old and new are the patterns
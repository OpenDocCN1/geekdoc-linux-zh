Now that you are comfortable with *groff*, you can look at two useful add-ons for *groff*: *geqn* and *gtbl*. In this chapter, you learn the following:

+   - What are *geqn* and *gtbl*?
- How to create complex equations easily.
- How to format tables for *groff* documents.

In the last chapter, you saw how *groff* is used to produce formatted documents for both screen and printer. Unfortunately, *groff* is not the easiest package to work with for complex problems such as tables and equations, so a set of macros for these tasks was developed.

The utilities *gtbl* and *geqn* are preprocessors which means that you write the source code as usual, but then the *gtbl* and *geqn* programs scan through and replace their specific commands with *groff* commands. Except for these specific commands, no other changes to the text or *groff* commands are performed.

# # geqn

The *geqn* preprocessor is designed for formatting complex equations and printing special symbols. You need only use *geqn* if you are using *groff* to create a document with these kinds of characters embedded within them.

Although *groff* has enough power to provide simple equations, it is not particularly friendly or powerful enough for more than single-line material. On the other hand, *geqn* is quite easy to work with. Most aspects of *geqn* are designed to look like equivalent English commands or words.

You can quickly move through a set of the important parts of *geqn*. As you will see, it is remarkably easy to work with.

# ## Executing geqn

The *geqn* preprocessor is invoked before the *groff* formatter. Usually, this is accomplished with a simple pipe command:

```
```
geqn filename | groff
```
```

This processes *filename* through *geqn*, which converts *geqn* commands to equivalent *groff* commands and then sends the result to *groff* for processing.

The command

```
```
geqn file1 file2 file3 | groff
```
```

processes three files and sends them all to *groff*.
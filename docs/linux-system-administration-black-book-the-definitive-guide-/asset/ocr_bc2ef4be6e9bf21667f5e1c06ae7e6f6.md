TIP: Type “which perl” to find the exact path on your machine. If nothing comes up, then you probably do not have Perl installed. See the Immediate Solutions section “Installing Perl” for directions on how to install it.

From here, of course, things get far more complicated. The following sections detail how to use specific aspects of the Perl language and syntax.

# In The Beginning

After the #! header, certain pieces of information typically belong at the beginning of a Perl script. Items that you also may want to have at the beginning of your Perl code are listed in Table 21.1.

> NOTE: The require statement expects files to have a .pm extension. If they do not, use the format require 'file.extension';

# Perl Basics

When you start writing Perl and shell scripts, you may find yourself having to look back and forth between this chapter and the previous one to double-check syntax. For example, to assign a value to a variable in Perl, you use the following format:

```
`$variable = value;`
```

A variable in Perl always has a dollar sign in front of it. For a string, you might use instead:

```
`$variable = "value";`
```

**Table 21.1** Starter pieces to a Perl script.
| Code | Description | Example |
| :--- | :--- | :--- |
| #comments | It is good form to explain the purpose of the program at the beginning of the document. This can save you a lot of digging through code as you try to remember what a program is supposed to do. | #This script calculates a customer's bill. |
| require | Loads code from the specified file at runtime. | require cgifunctions; |
| use | Loads the specified module so that you have access to its functions and commands. | use perl-cgi; |
| variable declarations | Many people find it efficient to keep all of their variable initializations at the beginning of a script. This way, if you need to go back later and adjust your initial settings, you can find them all in one place. | $cost = 1.24; |
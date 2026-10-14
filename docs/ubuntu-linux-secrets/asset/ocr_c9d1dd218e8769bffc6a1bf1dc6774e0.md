After you see the cpan> prompt you're ready to start using CPAN. You can now search CPAN for something useful.

Type h at the command prompt to see a list of available commands. Reading the help screen, you'll see that regular expressions can be used to search for a specific module. To search for a specific package with the regular expression, type

```
m /package/
```

> On each visit to the CPAN mirror, run the command reload index to ensure that you can access the latest modules to hit the mirror.

The CPAN module searches the database for modules that fit the search criteria, then lists the matching modules. To download and install a module, type

```
install modulename
```

CPAN will download the module, configure it for your system, and install all at once. If you prefer to download now and install later, use the get command instead of install. The h or ? command is always available to help you decide what to do next.

> The CPAN module offers a command history if ReadLine support is enabled. If it is, you can use your up and down arrows to repeat or edit a recent command.

When you have found and installed all the modules you want, type q at the cpan> prompt to quit the module and return to the shell command-line prompt.

# What Is Python?

The Python scripting language was created by Guido van Rossum, and first released to the public in 1991. It's actually not named after the reptile, but oddly, after the popular British comedy TV show Monty Python's Flying Circus. The naming of the project might give you a clue as to light-heartedness found in the Python programming culture. Yet for all the silliness, the language is responsible for some very hard-working tools.

Quality assurance teams for both computer hardware and software use Python scripts to get their products ready for release. Search engines (including Google) use Python to
(some believe that it is more *like peculariar)* and can generally be expressed as follows:

```
$ find [where to start looking?] [what to look for?] [what to do with it
when it's found]?<Enter>
```

The real syntax, though, is

```
$ find directory(ies) conditions<Enter>
```

The *conditions* could include or be called options, match criteria, actions, arguments, and all sorts of other designations. Nearly all information sources seem to have a different interpretation of what to call the required parameters, but their examples all look similar. Luckily, although no agreement exists on how to express the parameters for the `find` command, overall agreement does exist on how to use it.

# Example 8.1 Using find with Conditions

Since we last looked at Sancho’s directory structure, it has changed significantly. Recently, after some confusion while looking for maps and other data, Sancho has concluded that he relies on the filename `misc` maybe a little too much. To begin straightening things out, he wants to know how many times he has used it recently. Here is how he checks:

```
$ cd<Enter>
$ pwd<Enter>
/home/panzaasn
$ find -name misc -print<Enter>
./misc
./Misc/misc
./Maint/misc
./Admin/misc
```

Sancho first changed directories to return to his home directory. Then, he invoked the `find` utility, which began searching at the top of his home directory. He also specified `-print` at the end of the command line, which is interpreted as printing to *stdout* (standard output; that is, printing to the terminal screen). If he had not specified anything, the output would still have printed to his terminal by default. In earlier versions of UNIX and UNIX-like operating systems, though, this situation was not the case. You had to explicitly tell the shell what to do with the output.
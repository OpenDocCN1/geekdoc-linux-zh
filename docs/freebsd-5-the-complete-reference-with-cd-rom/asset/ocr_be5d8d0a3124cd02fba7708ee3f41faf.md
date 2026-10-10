> **Note** *Some programmers prefer not to refer to some or all of these languages as scripting languages. Indeed, compilers for some of these languages are available.*

Each of these scripting languages has its adherents, some of whom can be quite adamant that their chosen language is the One True Programming Language. I don't intend to debate this point, but for practical purposes, I must choose one language to use for examples in the rest of this chapter. Because it's available on all FreeBSD systems and because it's used by so many startup scripts, I use shell scripting for examples.

As you might guess, each shell provides its own shell scripting language. These languages implement the features of the shell in question, and thus differ somewhat from one shell to another. Thus, it's possible to write a `csh` shell script that won't work in the Korn shell, to name just one possible conflict. As a general rule, though, you should try to write shell scripts that don't rely upon specific shells' features. Indeed, many shell scripts will work when run from any common FreeBSD shell. As described earlier, in "Bridging the Gap," you can and should use the first line of the script to specify the shell you're using if you use features of a particular shell. Most scripts specify `/bin/sh` as their scripting language, so that's what I use as an example in this chapter.

> **Caution** *In FreeBSD, `/bin/sh` is a basic Bourne shell. On some other UNIX-like systems, though, `/bin/sh` may be something else. For instance, on most Linux systems, `/bin/sh` is a symbolic link to the Bourne Again Shell (Bash), which is an expanded relative of the Bourne shell. Thus, it's possible to run into scripting feature problems when transferring a script from one UNIX-like OS to another. Writing for a "plain" Bourne shell referred to as `/bin/sh` seldom causes problems. A Linux script that uses Bash-specific features may not work correctly on FreeBSD, though, unless you modify the script to point to Bash (`/usr/local/bin/bash` in FreeBSD).*

# Starting and Ending a Script

In addition to the codes in the first two bytes of a file identifying the file as a script, shell scripts normally have their execute permission bits set, as described in Chapter 8. Doing this enables you to type the name of the script to launch it. If you don't include execute permission, you can usually still run the script, but only by explicitly passing it to the shell in question. If you create a new script, therefore, you should set it to be executable with a command such as

```
```
$ chmod a+x myscript.sh
```
```

Many scripts end unceremoniously; they just stop. The most proper way to end a shell script, though, is with the `exit` command:

```
```
exit 0
```
```
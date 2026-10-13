The sed command also is designed to work using editing scripts. To make numerous, regular changes to files, create an editing script, and use your script to edit files. Use the sed command's -f, or script file, command-line option to use the script:

```
# sed -f myscript.sed < form.ltr >output.ltr
```

![](bbox=[0.22, 0.36, 0.28, 0.44])

> There are too many text filters included with your OpenLinux distribution to discuss in this hour; see the manual pages for the filter commands listed near the beginning of this section. You also might want to experiment with the wc, or word count, program, which reports the number of characters, words, and lines in your text documents.

# Spell Checking Your Documents

Misspelled words in your documents can be embarrassing, especially if other people read your text. Correct spelling is an important part of writing and word processing. Just as errors in syntax can cause programming errors, spelling errors can cause problems in miscommunication, loss of a potential job or customer, or the respect of a supervisor.

Fortunately, your Linux distribution comes with the ispell spelling checker, so you don't have to suffer the embarrassment of misspelling! This section shows you how to correct documents and fix your spelling errors.

# Correcting Documents with the ispell Command

The ispell command, found under the /usr/bin directory, is an interactive spelling program you can use alone or with your text editor to correct spelling mistakes. Several editors included with your Linux distribution, such as emacs and pico, are set up to automatically use this program for spell checking, but using ispell by itself is easy. For example, to check the spelling of the file myfile.txt, use the following:

```
# ispell myfile.txt
```

The ispell program loads the text and then displays the first found error in context, along with a single or several suggested replacements, as in this example:

```
MERCHANTABILITY          File: LICENSE

WARRANTIES, INCLUDING, WITHOUT LIMITATION, THE IMPLIED WARRANTIES OF
MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE.

? : MERCHANTIBILITY
[SP] <number> R)epl A)ccept I)nsert L)ookup U)ncap Q)uit e(X)it or ?
? for help
```
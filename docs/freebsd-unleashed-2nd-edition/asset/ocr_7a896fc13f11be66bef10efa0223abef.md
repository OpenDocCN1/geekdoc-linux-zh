Save this file somewhere (`/usr/local/libexec/if-ps` might be a good choice). Make the file executable so that `lpd` can run it (`chmod 555 /usr/local/libexec/if-ps` will do the trick).

This code reads the first line of the input it is sent by `lpd` and stores it in the variable `header`. The program then uses the `expr` command to get the first two characters from the file and stores them in the variable `ps_test`. The `if` statement that comes next checks what two characters are stored in `ps_test`. If they are `%!`, this is a PostScript file and the `then` statement is performed, which passes the raw data directly to the printer. It sends the first line, "cats" the rest of the input, sends an escaped `\004` with `printf`, and finally exits with a status of 0. The double ampersand (`&&`) connects the different statements and basically says, "Either do all of these commands or don't do any of them." If for whatever reason any part of this command line fails, none of it will be performed, and the program will exit with status 2 instead—which tells `lpd` that the data could not be printed and that it should not retry.

If the first two characters are not `%!`, this file is not a PostScript file, and the `else` statements are performed instead. The `else` statements in this case first `echo` the first line of the program and then "cat" the rest of the input and pipe it to `/usr/local/bin/a2ps`. The `a2ps` program does the work of converting the file into PostScript and sending it to the printer.

Finally, when all the data has been sent, an escaped `\004` is sent with `printf`, and the program exits with a status of 0. As with the `then` statement, if any part fails, the program will exit with a status of 2 instead.

The `a2ps` program has many options, so if you will be printing plain-text files through a PostScript printer on a regular basis, I suggest you read the man page for `a2ps`. You can then modify the way this script calls `a2ps` to suit your needs and preference.

# Printing PostScript Files on Non-PostScript Printers

If you have a non-PostScript printer, your problem is just the opposite of the one just described. You need to let plain text pass through to the printer, but you need to convert PostScript data to a format that your printer can understand.

If you never plan to print more than plain text, you do not need to worry about this. However, PostScript is the common denominator in Unix and FreeBSD when it comes to printing anything other than plain text. Virtually all word processing, graphing, drawing, and graphics programs can write a PostScript file (or send it directly to the printer).

Although some applications (such as StarOffice) may have drivers for your particular printer, most Unix applications will not. Instead, they will simply output PostScript. Because of this, your printing capabilities will be severely limited if you cannot handle PostScript.

Fortunately, a company called Aladdin makes a freely available program called GhostScript that can simulate a PostScript printer. It takes PostScript input and converts it to a form that your printer can understand.
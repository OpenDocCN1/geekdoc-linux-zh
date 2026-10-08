
## Using the wc Command

Use the `wc` command to count the number of lines (option `-l`), words (option `-w`), and bytes or characters (option `-c`) in text files. You may specify all three options in the command line, that is, `-lwc`. If you enter the command without options, you see counts of lines, words, and characters in that order. You can use the `wc` command to count the number of lines in a new file, `counters`.

To create a file and count its lines:

1. After the `$` command prompt, type `cat > counters` and press Enter.
2. Type this text, pressing Enter at the end of each line:
   ```
   Linux is a full featured UNIX clone.
   Linux blends the best of BSD and Sys V.
   ```
3. Type `Ctrl+D`.
4. To find the number of lines in `counters`, type `wc -l counters` and press Enter. UNIX reports that the file contains two lines.
5. To find the number of bytes in `counters`, type `wc -c counters` and press Enter. UNIX reports that the file contains 77 bytes.
6. To find the number of words in `counters`, type `wc -w counters` and press Enter. UNIX reports that the file contains 16 words.
7. To count words, characters, and lines in `counters`, type `wc -lwc counters` and press Enter. UNIX reports the counts for lines (2), words (16), and bytes (77).

## Using the Manipulate and Format Commands

In addition to the manipulate and format commands you used in Chapter 4, you can also use the `sed`, `tr`, and `pr` commands to edit and transform data's appearance before you display or print it.

### Introducing sed

When you want to make global changes to large files, you need a different kind of tool than interactive editors like `vi` and `Emacs`. Another UNIX editor, `sed`, is designed specifically for that purpose. The minimum requirements to run `sed` are an input file and a command that lets `sed` know what actions to apply to the file. `sed` commands have two general forms:

#### Syntax

```
sed [options] 'command' file(s)
sed [options] -f scriptfile file(s)
```

#### Dissection

- The first form lets you specify an editing command on the command line.
- The second form lets you specify a script file containing `sed` commands.

You can use `sed` to work with a new file, `unix_stuff`, to display only certain lines and to replace text.

To use `sed` to manipulate a file:

1. To create a new file, `unix_stuff`, in your working directory, type `cat > unix_stuff` and press Enter.
2. Type this text, pressing Enter at the end of each line:
   ```
   Although UNIX supports other database systems, 
   UNIX has never abandoned the idea of working with
   flat files. Flat files are those that are based on
   pure text with standard ASCII codes. Flat files
   can be read by any operating system.
   ```
3. Press `Ctrl+D`.
4. To display only lines 3 and 4, type `sed -n 3,4p unix_stuff` and press Enter. (The `n` option prevents `sed` from displaying any lines except those specified with the `p` command.) This means "find lines numbered (-n) 3 and 4 in the file Unix_stuff and display them (p)." You see lines 3 and 4:
   ```
   flat files. Flat files are those that are based
   on pure text with standard ASCII codes. Flat files
   ```
5. In `sed`, you can place two commands on one line. If you want to delete lines 3 and 4 and then display the file, you must use `sed`'s `-e` option to specify multiple commands on the same line.
6. To delete lines 3 and 4 from `unix_stuff` and display the results, type `sed -n -e 3,4d -e p unix_stuff` and press Enter. You see the text:
   ```
   Although UNIX supports other database systems,
   UNIX has never abandoned the idea of working with
   can be read by any operating system.
   ```
   Note: Lines 3 and 4 are not actually deleted from the file but simply filtered out so they are not displayed.
7. To display only lines containing the word, “Flat,” type `sed -n /Flat/p unix_stuff` and press Enter. You see the text:
   ```
   flat files. Flat files are those that are based on pure text with standard ASCII codes. Flat files
   ```
8. To replace all instances of the word “Flat” with “Text,” type `sed -n s/Flat/Text/p unix_stuff` and press Enter. (The `s` command substitutes one string of characters for another.) You see the text:
   ```
   flat files. Text files are those that are based on pure text with standard ASCII codes. Text files
   ```

To append new lines in `sed`, you must use the `a\` command. This command appends lines after the specified line number. Like all other `sed` commands, it operates on all lines in the file if you do not specify a line number. Next you can create a new script file, `more_stuff`. Include the append command, `a\`, in the file with the lines to be appended to the file `unix_stuff`. You must terminate each line, except for the last line of the file being added, with a backslash character. In the next steps, the `$` preceding the `a\` symbol tells `sed` to append `more_stuff` to `unix_stuff` after the last line in `unix_stuff`; without `$`, `sed` repeatedly adds all the lines in `more_stuff` after each line in `unix_stuff`.

To create a script file to append lines to another file:

1. To create the script file `more_stuff`, type `cat > more_stuff` and press Enter.
2. Type this text, pressing Enter at the end of each line:
   ```
   $a\
   Informix and Oracle, two major relational database\ companies have installed their RDBMS packages on UNIX\ systems for many years.
   ```
3. Press `Ctrl+D`.
4. To use the `sed` command to run the script file, type `sed -f more_stuff unix_stuff` and press Enter. You see this text:
   ```
   Although UNIX supports other database systems, UNIX has never abandoned the idea of working with flat files. Flat files are those that are based on pure text with standard ASCII codes. Flat files can be read by any operating system. Informix and Oracle, two major relational database
   companies have installed their RDBMS packages on UNIX systems for many years.
   ```
5. Use `vi` to create the file `stuff_replace`. Insert the following `sed` commands into the file:
   ```bash
   s/UNIX/Linux/
   s/abandoned/given up/
   s/standard/regular/
   ```
   The lines in the file instruct `sed` to replace all occurrences of “UNIX” with “Linux,” “abandoned” with “given up,” and “standard” with “regular.”
6. Execute `sed`, with the script file you created in Step 5, on the `unix_stuff` file. Redirect `sed`'s output to the file `unix_stuff2`. Type `sed -f stuff_replace unix_stuff > unix_stuff2` and press Enter.
7. Type `cat unix_stuff2` and press Enter. You see the file with the changes specified by the `stuff_replace` script file.

## Translating Characters Using the tr Command

The `tr` command copies data from the standard input to the standard output, substituting or deleting characters specified by options and patterns. The patterns are strings and the strings are sets of characters.

| **Syntax** | `tr [options] string1 string2` |
| :--- | :--- |
| **Dissection** | - In its simplest form, `tr` translates each character in *string1* into the character in the corresponding position in *string2*. The strings may need to be “quoted” with either single or double quotes. |
| | - Two options used most frequently are `-d` (delete character) and `-s` (substitute character). |

A popular use of `tr` is converting lowercase characters to uppercase characters. You can translate the file `counters` from lowercase to uppercase characters by specifying `[a-z]` as the lowercase characters and `[A-Z]` as the uppercase characters.

To translate lowercase characters to uppercase characters in the file `counters`:
- After the `$` command prompt, type `tr [a-z] [A-Z] < counters` and press Enter.
You see these lines:
```
LINUX IS A FULL FEATURED UNIX CLONE.
LINUX BLENDS THE BEST OF BSD AND SYS V.
```

You can also use the `-d` option with the `tr` command to delete input characters found in *string1* from the output. This is helpful when you need to remove an erroneous character from the file.

To delete specified characters from the `counters` file:
- To delete the characters “full” from the output, type `tr -d "full" < counters` and press Enter.
You see this text:
```
Linx is a eated UNIX cone.
Linx bends the best o BSD and Sys V.
```
Notice that the command deleted all characters in “full”---every f, u and l---from the output, rather than occurrences of the word “full”.

The `-s` option of the `tr` command checks for sequences of a *string1* character repeated several consecutive times. When this happens, `tr` replaces the sequence of repeated characters with one occurrence of the corresponding character from *string2*. For example, use the `-s` option when you need to change a field delimiter in a flat file from one character to another. For example, in the file `zoo2`, use `tr` to replace the field delimiter “:” with a space character, “ ”. First, use `cat` to display the file.

To replace characters in the file `zoo2`:
1. After the `$` command prompt, type `cat zoo2` and press Enter.
   You see this text:
   ```
   Monkeys:Bananas:2000:850.00
   Lions:Raw Meat:4000:1245.50
   Camels:Vegetables:2300:564.75
   Elephants:Hay:120000:1105.75
   ```
2. Type `tr -s ":" " " < zoo2` and press Enter.
   You see this text:
   ```
   Monkeys Bananas 2000 850.00
   Lions Raw Meat 4000 1245.50
   Camels Vegetables 2300 564.75
   Elephants Hay 120000 1105.75
   ```

## Using the pr Command to Format Your Output

The `pr` command prints the specified files on the standard output in paginated form. If you do not specify any files or you specify a filename of “-”, `pr` reads the standard input.

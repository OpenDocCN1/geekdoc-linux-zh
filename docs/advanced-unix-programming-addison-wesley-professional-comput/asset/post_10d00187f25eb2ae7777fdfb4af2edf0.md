
```c
case 0: /* child */
    switch (pid2 = fork()) {
    case -1:
        EC_FAIL
    case 0: /* grandchild */
        ec_neg1( dup2(pfd[0], STDIN_FILENO) )
        ec_neg1( close(pfd[0]) )
        ec_neg1( close(pfd[1]) )
        exec1p("wc", "wc", "-1", (char *)NULL);
        EC_FAIL
    }
    /* still the child */
    ec_neg1( dup2(pfd[1], STDOUT_FILENO) )
    ec_neg1( close(pfd[0]) )
    ec_neg1( close(pfd[1]) )
    exec1p("who", "who", (char *)NULL);
    EC_FAIL
    /* parent */
    ec_neg1( close(pfd[0]) )
    ec_neg1( close(pfd[1]) )
    ec_neg1( waitpid(pid1, NULL, 0) )
    return;
EC_CLEANUP_BGN
EC_FLUSH("who_wc2*");
EC_CLEANUP_END
```

Two points about this example:

- The child has to create the grandchild before closing the reading file descriptor so the grandchild will inherit it.
- The parent waits only for who (pid1) to terminate. It can't wait for wc because wc is not its child. The child running who can't wait for wc either because the who program hasn't been designed to do that. Putting a call to waitpid after the call that execs wc won't help because on a successful exec all the code are overwritten. What happens (as explained in Section 5.8) is that when who (wc's parent) terminates, a system process will inherit wc and will wait for it.

We could just as easily have reversed things and made wc the parent of who (see Exercise 6.11).

Of course, it's much easier to use a shell to set up a command line like this than it is to write a custom program. In the next section we'll code such a shell.

## 6.4 A Real Shell

Our shell is a subset of the typical UNIX shell that you probably use. It has these features:

- A *simple command* consists of a command name followed by an optional sequence of arguments separated by spaces or tabs, each of which is a single word or a string surrounded by double quotes (`"`). If quoted, an argument may include any otherwise special characters (`|`, `;`, `&`, `>`, `<`, space, tab, and newline). An included quote or backslash must be preceded by a backslash (`\"` or `\\`). A command may have up to 50 arguments, each of which may have up to 500 characters.
- A simple command's standard input may be redirected to come from a file by preceding the file name with `<`. Similarly, the standard output may be redirected with `>`, which truncates the output file. If the output redirection symbol is `>>`, the output is appended to the file. An output file is created if it doesn't exist.
- A *pipeline* consists of a sequence of one or more simple commands separated by bars (`|`). Each except the last simple command in a pipeline has its standard output connected, via a pipe, to the standard input of its right neighbor.
- A pipeline is terminated with a newline, a semicolon (`;`), or an ampersand (`&`). In the first two cases the shell waits for the rightmost simple command to terminate before continuing. In the ampersand case, the shell does not wait. It reports the process number of each simple command in the pipeline, and each simple command is run with interrupt and quit signals ignored.
- Built-in commands are assignment, `set`, and `cd`. The first two of these were described in Section 5.4. `cd` works in the familiar way.

The first step is to parse input lines into *tokens*, which are groups of characters that form syntactic units; examples are words, quoted strings, and special symbols such as `&` and `>>`. Each token is represented by a symbolic constant, as follows:

- `T_WORD`: An argument or file name. If quoted, the quotes are removed after the token is recognized.
- `T_BAR`: The symbol `|`.
- `T_AMP`: The symbol `&`.
- `T_SEMI`: The symbol `;`.
- `T_GT`: The symbol `>`.
- `T_GTGT`: The symbol `>>`.
- `T_LT`: The symbol `<`.
- `T_NL`: A newline.
- `T_EOF`: A special token signifying that the end-of-file has been reached. If the standard input is a terminal, the user has typed an EOT (Ctrl-d).
- `T_ERROR`: A special token signifying an error.

The job of a *lexical analyzer* is to read the input and assemble the characters into tokens. Each time it is called, one token is returned. If the token is T_WORD, a string containing the actual characters composing it is also returned. (For the other tokens the actual characters are obvious.) The lexical analyzer should bypass irrelevant characters, such as spaces separating arguments, without returning anything.^[4]

Our lexical analyzer is a finite-state-machine: As characters are read they are either recognized immediately as tokens or they are accumulated (characters of a word, for example). With each character, the lexical analyzer can switch into a new state which serves to remember what it is doing and how characters are to be interpreted. For example, when accumulating a quoted string, spaces are treated differently than when they appear outside quotes. For our shell we need four states:

- `NEUTRAL`: The starting state for each call to the lexical analyzer. Spaces and tabs are skipped. The characters `|`, `&`, `;`, `<`, `>` and newline are recognized immediately as tokens. The character `>` causes a switch to state GTGT, which will see if it is followed by another `>`, since `>` and `>>` are two different tokens. A quote causes a switch to state INQUOTE, which gathers a quoted string. Anything else is taken as the beginning of an unquoted word; the character is saved in a buffer and the state is switched to INWORD.

^[4] Most UNIX systems include a command called `lex` that can automatically generate a lexical analyzer from a description of the tokens it is to recognize. Because `lex` is complicated to use, and because the lexical analyzers it generates are sometimes big and slow, it's usually preferable to code lexical analyzers by hand. They aren't difficult programs to write.

- `GTGT`: This state means that `>` was just read. If the next character is also `>`, the token T_GTGT is returned. Otherwise, T_GT will be returned. But first, we’ve read one character too many, so we put it back on the input with the Standard C function `ungetc`.
- `INQUOTE`: This state means that a starting quote was read. We accumulate characters into a buffer until the closing quote is read. Then we return the token T_WORD and the accumulated string. Special steps must be taken to process the escape character `\`.
- `INWORD`: This state means that the first character of a word was read and has been put into the buffer. We keep accumulating characters until a nonword character is read (`,` say). We put the gratuitous character back on the input and return the token T_WORD.

With this explanation, the code for our lexical analyzer, `gettoken`, should be readily understandable:

```c
typedef enum (T_WORD, T_BAR, T_AMP, T_SEMI, T_GT, T_GTGT, T_LT, T_NL, T_EOF, T_ERROR) TOKEN;

static TOKEN gettoken(char *word, size_t maxword)
{
    enum (NEUTRAL, GTGT, INQUOTE, INWORD) state = NEUTRAL;
    int c;
    size_t wordn = 0;

    while ((c = getchar()) != EOF) {
        switch (state) {
        case NEUTRAL:
            switch (c) {
            case ';':
                return T_SEMI;
            case '&':
                return T_AMP;
            case '|':
                return T_BAR;
            case '<':
                return T_LT;
            case '\n':
                return T_NL;
            case '\t':
                continue;
            case '>':
                state = GTGT;
                continue;
            case '"':
                state = INQUOTE;
                continue;
            default:
                state = INWORD;
                ec_false( store_char(word, maxword, c, &wordn) )
                continue;
            }
        case GTGT:
            if (c == '>')
                return T_GTGT;
            ungetc(c, stdin);
            return T_GT;
        case INQUOTE:
            switch (c) {
            case '\\':
                if ((c = getchar()) == EOF)
                    c = '\\';
                ec_false( store_char(word, maxword, c, &wordn) );
                continue;
            case '"':
                ec_false( store_char(word, maxword, '\0', &wordn) )
                return T_WORD;
            default:
                ec_false( store_char(word, maxword, c, &wordn) )
                continue;
            }
        case INWORD:
            switch (c) {
            case '/':
            case ',':
            case ']':
            case '<':
            case '>':
            case '\n':
            case '"':
            case '\t':
                ungetc(c, stdin);
                ec_false( store_char(word, maxword, '\0', &wordn) )
                return T_WORD;
            default:
                ec_false( store_char(word, maxword, c, &wordn) )
                continue;
            }
        }
    }
    ec_false( !ferror(stdin) )
    return T_EOF;
}
```

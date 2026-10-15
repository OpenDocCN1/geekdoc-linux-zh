```
B  describe-bindings. Display table of all key bindings.
C  describe-key-briefly. Type a command key sequence;
    it prints the function name that sequence runs.
F  describe-function. Type a function name and get documentation of it.
I  info. The info documentation reader.
K  describe-key. Type a command key sequence;
    it displays the full documentation.
L  view-lossage. Shows last 100 characters you typed.
M  describe-mode. Print documentation of current major mode,
    which describes the commands peculiar to it.
N  view-emacs-news. Shows emacs news file.
S  describe-syntax. Display contents of syntax table, plus explanations
T  help-with-tutorial. Select the Emacs learn-by-doing tutorial.
V  describe-variable. Type name of a variable;
    it displays the variable's documentation and value.
W  where-is. Type command name; it prints which keystrokes
    invoke that command.
---*Emacs: *Help*          (Fundamental)--Top----
A B C F I K L M N S T V W C-x  b C-d C-n C-w or Space to scroll: _
```

What to do now? Seventeen options are possible from this point, as shown in Table 12.4.

| Command | Meaning |
|---|---|
| A | List all commands matching the specified word. |
| B | List all key mappings. |
| C | Describe any key sequence pressed instead of doing it. |
| F | Describe the specified function. |
| I | Start the info browser. |
| K | Fully describe the result of a particular key sequence. |
| L | Show the last 100 characters you typed. |
| M | Describe the current mode you're in. |
| N | Show the emacs news file. |
| S | List a command syntax table. |
| T | Start the emacs tutorial. |
| V | Define and describe the specified variable. |
| W | Indicate what keystroke invokes a particular function. |
| C-x b | Display emacs copyright and distribution information. |
| C-d | Display emacs ordering information. |
| C-n | Display recent emacs changes. |
| C-w | Display the emacs warranty. |

# TABLE 12.4 emacs Help System Command Options

2. I choose K and then press M-< to see what that command really does. The first thing that happens after I type K is that the table of help information vanishes, to be replaced by my original text, and then the prompt appears along the bottom:
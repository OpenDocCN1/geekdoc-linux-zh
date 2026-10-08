# csh 199

^previous-word replacement^
Repeat the previous command line, replacing the string
previous-word with the string replacement. This is equivalent to the
history substitution: !s/previous-word/replacement/
to execute a specific previous command and make such a
substitution, say, reexecuting command #6,
!:6s/previous-word/replacement./

# Word Designators

A colon (:) separates the event specification from the word designator. You can omit if
t word designator begins with a ^, $, *, or %. If the word is to be selected from
previous command, you can omit the second character from the event specification. For
instance, !!1 and !!1 both refer to the first word of the previous command, whereas
!! and $ both refer to the last word in the previous command. Word designators
include:

+   # The entire command line typed so far.
0 The first input (command).
n The $n$-th argument.
^ The first argument, that is, 1.
$ The last argument.
% The word matched by (the most recent) ?s search.
x-y A range of words: -y abbreviates 0-y.
* All arguments, or a null value if there is one word in the event.
x-^ Abbreviates x-.
x-^ Like x-^ but omitting word $

# Modifiers

After the optional word designator, you can add one of the following modifiers, preceded
by a colon (:).

+   h Remove a trailing path name component, leaving the head.
r Remove a trailing suffix of the form .xxx leaving the basename.
e Remove all but suffix, leaving the extension.
s/l/r/ Substitute r for l/.
t Remove all leading path-name components, leaving the tail.
& Repeat the previous substitution.
g Apply the change to the first occurrence of a match in each word by
prefixing the above (for example, g&).
p Print the new command but not execute it.
q Quote the substituted words, escaping further substitutions.
x- Like q, but break into words at each space character, Tab, or newline.
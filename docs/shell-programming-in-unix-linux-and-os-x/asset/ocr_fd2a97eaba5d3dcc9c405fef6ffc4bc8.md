indicates it's a substitution, the slashes delimit the old and new values, and g indicates it should
be applied as many times as needed for each line, not just once per line.

# Matching the Beginning of the Line: The Caret (^)

When the caret ^ is used as the first character in a regular expression, it matches
beginning of the line. So the regular expression

^George

matches the characters George only if they occur at the beginning of the line. This is actually
known as "left-routing" in the regex world, for obvious reasons.

Let's have a look:

```
$ ed intro
248
/the/
>>in the late 1960s. One of the primary goals in
>>the design of the Unix system was to create an
Find the line that starts with the
/the/
design of the Unix system was to create an
Insert>> at the beginning of each line
1,$/^
>>The Unix system was pioneered by Ken
>>Thompson and Dennis Ritchie at Bell Laboratories
>>in the late 1960s. One of the primary goals in
>>the design of the Unix system was to create an
>>environment that promoted efficient process
>>development.
```

The preceding example also shows how the regular expression ^ can be used to match the
beginning of the line. Here it is used to insert the characters >> at the start of each line.
A command

```
1,$*/' /
```

is commonly used to insert spaces at the start of each line (in this case four spaces were
(inserted).

# Matching the End of the Line: The Dollar Sign $

Just as the ^ is used to match the beginning of the line, so the dollar sign $ is used to match
the end of the line. So the regular expression

```
contents$$
```

matches the characters contents only if they are the last characters on the line. What do you
think would be matched by the regular expression

$
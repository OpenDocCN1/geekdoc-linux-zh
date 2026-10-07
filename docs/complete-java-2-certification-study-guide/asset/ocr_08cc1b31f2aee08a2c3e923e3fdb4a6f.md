# Scanning and Formatting Text 295

The string contains invariant text and formatting instructions for the values. Let's look at a simple
example:

```
StringBuilder sb = new StringBuilder();
Formatter f = new Formatter(sb);
boolean b = false;
f.format('The value is %b, so there. ', b);
System.out.println(sb);
```

The output is

The value is false, so there.

The format() calls its first argument as a guideline. Any text up to a special character
is appended literally to the string builder. The % sign is a special code that indicates the
method's second argument is to be formatted and inserted into the text. The argument index is
followed by a dollar sign ($), which is followed by formatting. In the simplest cases,
formatting information is a single letter. The format codes you need to know about the
amare these:

+   * %b a value (wrapper or primitive)
* %c an integer
* %d a floating-point number
* %s an object, generally by calling its toString() method

Now you can see how our first example worked. The format string was appended
to the string builder until the %b code was reached. This meant that the method's second argu-
to to be formatted as text representing a boolean value and appended to the string
builder. After that the remainder of the format string (since it has no more special characters)
was to be appended.
If a format string has more than one special character, the formatter expects the format()
method to have one argument for each special character. By default, they are formatted in the
order of appearance. For example, here's a format string with two format codes and two add-	ional arguments:

```
StringBuilder sb = new StringBuilder();
Formatter f = new Formatter(sb);
boolean b = false;
f.format('Would you like some %F? %b', Math.PI, true);
System.out.println(sb);
```

The output is

Would you like some 3.1415937 true
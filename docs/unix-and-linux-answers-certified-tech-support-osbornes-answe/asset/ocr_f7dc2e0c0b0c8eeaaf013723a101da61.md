# Is there a way I can repeat my last text change?

Yes; use the dot command (.). This little trick saves loads of time. Need to add a couple of spaces at the beginning of the next several lines? Well, you could figure out the exact command sequence and write a macro to do it (see "Macros" later in this chapter), or just do an I Escape ("I", space, ESC) on the current line, press j to move down to the next one, and press . (dot). Do this for as many lines as you need to indent.

# SEARCHING FOR (AND REPLACING) TEXT

# What’s the easiest way to find some text?

Ah, now we get into external mode. Here we use the ex command set. So, to search from the current cursor position for something we use

```
/searchpattern
```

To search backwards, use

```
?searchpattern
```

The search pattern can be a simple bit of text, like searching for the word "Priscilla" in a file, or a more complicated pattern-matching string. Let’s save the pattern-matching discussion for just a moment.

# Can I search for and replace text?

Certainly. Search for one pattern and replace it with another, using the external mode substitute command. The syntax is

```
x,ys/searchpattern/replace/options
```
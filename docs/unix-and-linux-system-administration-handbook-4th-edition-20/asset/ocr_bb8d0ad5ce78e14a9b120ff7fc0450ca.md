# Chapter 2 Scripting and the Shell

There's a lot to see in just these few lines. At the risk of blurring laser-like focus, we include several common idioms in each of our Perl examples. We explain the tricky parts in the text following each example. If you read the examples carefully (don't be a wiper, they're short!), you'll have a working knowledge of the most common Perl forms by the end of this chapter.

# Array and string literals

In this example, notice first that (...) creates a literal list. Individual elements of the list are strings, and they're separated by commas. Once the list has been created, it is assigned to the variable @items.

Perl does not require that all strings be quoted. In this particular case, the initial assignment of @items works just without the quotes.

```
@items = (socks, shoes, shorts);
```

Perl calls these unquoted strings "barewords," and they're an interpretation of last resort. If something doesn't make sense in any other way, Perl tries to interpret it as a string. In a few limited circumstances, this makes sense and keeps the code clean. However, this is probably not one of those cases. Even if you prefer to quote strings constantly; be prepared to decode other people's quoteless code.

The More Perl way to initialize an array is with qw (quote strings) operator. It is in fact a form of string quotation, and like most quoted entries in Perl, you choose your own delimiters.

```
@items = qw(socks shoes shorts);
```

is the most traditional, but it's a bit misleading the part after the qw is no longer a list. It is in fact a string to be split at whitespace to form a list. The version

```
@items = qw[socks shoes shorts];
```

works, too, and is perhaps a bit truer to the spirit of what's going on. Note that the commas are gone since their function has subsumed by qw.

# Function calls

Both print and printf accept any number of arguments, and the arguments are separated by commas. But there's that join(...) thing that looks like some kind of function call; how is it different from print and print? Perl allows you to omit the parentheses in function calls when this does not cause ambiguity, so both forms are common. In the print line above, the parenthesized form distinguishes the arguments from join from that go to.

In, it's not; print, printf, and join are all plain-vanilla functions. We can tell that the expression @items[0] must evaluate to some kind of list it starts with. This is in an "array slice" or subarray, and the 0,1 script lists the indices of the elements to be included in the slice. Perl accepts a range of values here, too, as in the equivalent expression @items[0]. A single
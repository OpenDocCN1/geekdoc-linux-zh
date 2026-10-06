that string as it travels toward standard output, and it all seamlessly together. This is done by dropping formatting codes into the base string, and then passing a data item to printf for each of those codes, along with the base string. A formatting code begins with a percent sign and includes information relating to the type and size of the data item being merged with the base string, as well as how that information should be presented.

Let's look at a very simple example to start out. Here's a base string containing one formatting code:

> "The answer is %d, and don't forget it!"

 %d formatting code simply tells printf to convert a integer value to text, and substitute that for the formatting code in the base string. Of code, you must now pass an integer value to the base string (and I show you that's done shortly), but when you, printf will convert the integer to merge it with the base string as it sends text to the stream. If the decimal value passed is 42, on your screen you'll see this:

> The answer is 42, and don't forget it!

A formatting code actually has a fair amount of structure, and the printf mechanism as a whole has more wrinkles than I room here to describe. Any good C reference will explain the whole thing in detail—one more reason why it's useful to know C before you attempt Linux assembly work. Table 13.2 lists the most common and useful ones.

The most significant enhancement you can make to the formatting codes is to place an integer value between the % symbol and the code letter:

```
%5d
```

| Table 13.2 Common printf Formatting Codes |
| CODE | BASE | DESCRIPTION |
|---|---|---|
| %c | n/a | Displays a character as a character |
| %d | 10 | Converts an integer and displays it in decimal |
| %s | n/a | Displays a string as a string |
| %x | 16 | Converts an integer and displays it in hex |
| %% | n/a | Displays a percent sign |
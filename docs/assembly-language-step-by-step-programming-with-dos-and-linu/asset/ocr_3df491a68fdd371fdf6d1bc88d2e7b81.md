# ASSEMBLY LANGUAGE STEP-BY-STEP

If your program sends text to standard output (which is what happens by default), you can redirect your output to a text file when executing the program on the Unix command line:

```
# /eatlinux > eetext.txt
```

Here, instead of appearing on your screen, the text displayed by the EATLINUX program is sent to the text file eetext.txt.

I don't have the room in this book to discuss how to programmatically redirect the standard streams to other sources or destinations, but any good book on Unix or Linux C programming will explain it in detail. Like most everything else, it's nothing more complex than a function call.

# Formatted Text with printf

The puts library routine may seem pretty useful, but compared to a few of its more sophisticated siblings, it's kid stuff. With puts you can only send a simple text string to a stream, without any sort of formatting. Worse, puts always includes a newline at the end of its display, which you include one in your displayed string or not. (Notice when you run the executable program EATLINUX that there is a blank line after its output. That's the second newline, inserted by the puts routine.) This prevents you from using multiple calls to puts to output several strings all on a single line.

About the best you can say for puts is that it has the virtue of simplicity. For nearly all of your character output needs, you're better off using a much more powerful library routine: printf. The printf routine allows you to do a number of truly useful things, all with one function call:

+   - Output text without a newline

+   - Convert numeric data to text in numerous formats by passing codes along with the data

+   - Output text to a stream that includes multiple strings separately

If you've worked with C for more than half an hour, printf will be perfectly obvious to you, but for people coming from other languages (such as Pascal, which has no direct equivalent), it may take a little explaining.

The printf routine will gladly display a simple string like "Eat at Joe's"—but you can merge other text strings and converted numeric data with
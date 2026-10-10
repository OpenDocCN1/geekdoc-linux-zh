# LISTING 28.1 The Real Economics of Oil as it Appears in LaTeXX

```
\documentclass{article}
\title{The Real Economics of Oil}
\author{David Schowering}
\date{February 1972}
\begin{document}
\maketitle
Oil is subject to the supply and demand curves in an absolutely linear manner.
The more oil that is available at a given time, the lower cost of that oil.
The only modification to this absolutely linear
supply / demand curve is that which
is caused
by intervention of a government.
\end{document}
```

Now I know what you are going to say. “Gee it seems like a lot of gobbledygook and a lot more work.” Well, if you will try it, I am sure that you will find that, even on this small “document,” the results are worth it, and you can save time.

What you need to do is the following. Open your favorite editor or word processor. I used vi because I have been using it for 25 years, but WordPerfect or Star Office will produce the same results. Now, enter the text exactly as you see it in the preceding example. Note that *braces* are used around words in lines beginning with the \_non parentheses. When you are done, save the file as a text file with the extension _.tex*. This extension makes everything that follows much easier, but if you want to use any other extension for your own purposes, it will work.

Note that in the example I have interspersed carriage returns at odd places in the sentences. This is to remind you that with LaTeX you concentrate on the content of your document and not the physical formatting.

Now, let’s put LaTeX to the test. At the command line, enter the following command:

```
#latex [filename]
```

Or, use the .tex extension:

```
#latex [filename.extension]
```

On your terminal screen, you will see information similar to that shown in Figure 28.1.

If you don’t have any lines that begin

```
! LaTeX Error
```

everything is OK (well, maybe not the spelling of the words, but that can be fixed).
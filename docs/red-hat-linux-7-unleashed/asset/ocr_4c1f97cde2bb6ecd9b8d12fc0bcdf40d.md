You could perhaps do it by creating a temporary file:

```
echo $VARIABLE >$TMPFILE
tr [a-z] [A-Z] $TMPFILE
```

one_command is a two-line shell script written earlier in the day to process SQL commands. Why not inline the body of that script here? Although technically feasible, I have a strong preference for small, simple programs that are easy to understand and correspondingly easy to implement correctly. one_command already has been verified to do one small job reliably, so the script lets it do that job. This fits with the UNIX tradition that counsels combining robust toolkit pieces to construct grander works.

In fact, notice that the example in Listing 26.1 shows the shell’s nature as a “glue” language. There’s a small amount of processing within the shell in manipulating filenames, and then most of the work is handed off to other commands; the shell just glues together results. This is typical and is a correct style you should adopt for your own scripting.

Certainly, it was pleasant when the filenames changed and I realized I could rework one word of the script, rather than retype the 200 entries. As satisfying as this was, the total benefit of automation is still more profound. Even greater than saving my time are the improvements in quality, traceability, and reusability this affords. With the script, I control the data entering the database at a higher level and eliminate whole categories of error: mistyping, accidentally pushing a wrong button in a graphical user interface, and so on. Also, the script in Listing 26.1 records my procedure, in case it’s later useful to audit the data. Suppose, for example, that next year it’s decided I shouldn’t have inserted any of these references to the database’s $Picture attribute. How many will have to be backed out? Useful answers—at most, the count of $DIR/* .jpg—can be read directly from the script; there’s no need to rely on memory or speculation.

# # Tips for Improving Automation Technique

You’re in charge of your career in automation. Along with everything else this chapter advises, you’ll go furthest if you do the following:

+   - Improve your automation technique.
+   - Engineer well.

These tips have specific meaning in the rest of this chapter. Look for ways to apply them in all that follows.